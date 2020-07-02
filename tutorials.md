---
layout: default
title: Tutorials 
filename: tutorials.md
---

### Subject-specific 10 x 10 cross-validation on BCIC Dataset
The code below shows how to perform 10 x 10 cross-validation using on the BCI Competition Dataset IV 2a using this toolbox. In the `mainPipeline.py`, create an instance of the `MLEngine` class by passing the details of the data folder as follows:

`
from bin.MLEngine import MLEngine

dataset_details={
'data_path' : "/Data/BCICIV_2a_gdf", #path to data folder 
'file_to_load': 'A01T.gdf', #filename to load and perform cross-validation
'ntimes': 10,
'kfold':10,
'm_filters':2, 'window_details':{'tmin':0.5,'tmax':2.5}
}
ML_experiment = MLEngine(**dataset_details) ML_experiment.experiment()
`

In `MLEngine.experiment`, use the code below:

`
        bcic_data = LoadData.LoadBCIC(self.file_to_load, self.data_path)
        eeg_data = bcic_data.get_epochs()

        fbank = FilterBank(eeg_data.get('fs'))
        fbank_coeff = fbank.get_filter_coeff()
        filtered_data = fbank.filter_data(eeg_data.get('x_data'),self.window_details)
        y_labels = eeg_data.get('y_labels')

        training_accuracy = []
        testing_accuracy = []
        for k in range(self.ntimes):
            '''for N times x K fold CV'''
            train_indices, test_indices = self.cross_validate_Ntimes_Kfold(y_labels,ifold=k)
            '''for K fold CV by sequential splitting'''
            # train_indices, test_indices = self.cross_validate_sequential_split(y_labels)
            for i in range(self.kfold):
                train_idx = train_indices.get(i)
                test_idx = test_indices.get(i)
                print(f'Times {str(k)}, Fold {str(i)}\n')
                y_train, y_test = self.split_ydata(y_labels, train_idx, test_idx)
                x_train_fb, x_test_fb = self.split_xdata(filtered_data, train_idx, test_idx)

                y_classes_unique = np.unique(y_train)
                n_classes = len(np.unique(y_train))

                fbcsp = FBCSP(self.m_filters)
                fbcsp.fit(x_train_fb,y_train)
                y_train_predicted = np.zeros((y_train.shape[0], n_classes), dtype=np.float)
                y_test_predicted = np.zeros((y_test.shape[0], n_classes), dtype=np.float)

                for j in range(n_classes):
                    cls_of_interest = y_classes_unique[j]
                    select_class_labels = lambda cls, y_labels: [0 if y == cls else 1 for y in y_labels]

                    y_train_cls = np.asarray(select_class_labels(cls_of_interest, y_train))
                    y_test_cls = np.asarray(select_class_labels(cls_of_interest, y_test))

                    x_features_train = fbcsp.transform(x_train_fb,class_idx=cls_of_interest)
                    x_features_test = fbcsp.transform(x_test_fb,class_idx=cls_of_interest)

                    classifier_type = SVR(gamma='auto')
                    classifier = Classifier(classifier_type)
                    y_train_predicted[:,j] = classifier.fit(x_features_train,np.asarray(y_train_cls,dtype=np.float))
                    y_test_predicted[:,j] = classifier.predict(x_features_test)


                y_train_predicted_multi = self.get_multi_class_regressed(y_train_predicted)
                y_test_predicted_multi = self.get_multi_class_regressed(y_test_predicted)

                tr_acc =np.sum(y_train_predicted_multi == y_train, dtype=np.float) / len(y_train)
                te_acc =np.sum(y_test_predicted_multi == y_test, dtype=np.float) / len(y_test)


                print(f'Training Accuracy = {str(tr_acc)}\n')
                print(f'Testing Accuracy = {str(te_acc)}\n \n')

                training_accuracy.append(tr_acc)
                testing_accuracy.append(te_acc)

        mean_training_accuracy = np.mean(np.asarray(training_accuracy))
        mean_testing_accuracy = np.mean(np.asarray(testing_accuracy))

        print('*'*10,'\n')
        print(f'Mean Training Accuracy = {str(mean_training_accuracy)}\n')
        print(f'Mean Testing Accuracy = {str(mean_testing_accuracy)}')
        print('*' * 10, '\n')
`

In order to use MIBIF feature selection, use `Classifer.feature_selection = True`. The `FeatureSelect.fit()` method can be kept as follows:

`    
   def fit(self,x_train_features,y_train):
        MI_features = self.MIBIF(x_train_features, y_train)
        MI_sorted_idx = np.argsort(MI_features)[::-1]
        features_selected = MI_sorted_idx[:self.n_features_select]

        paired_features_idx = self.select_CSP_pairs(features_selected, self.n_csp_pairs)
        x_train_features_selected = x_train_features[:, paired_features_idx]
        self.features_selected_indices = paired_features_idx

        return x_train_features_selected
'

Using the above settings on each subject (the compeition training data, i.e., filenames ending with 'T') should produce the rsults below. Note that for reproducibility, the random seed value for every ntimes has been fixed as the index of that fold.

