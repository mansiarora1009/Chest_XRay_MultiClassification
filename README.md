# Chest-X-Ray-Disease-Diagnosis

Team 32 : Chest X-Ray disease classification Project
Members: Adiki Madhu Babu, Mansi Arora, Srinivas Sekar

Note: Use python3.6


Instructions to run each file are given below

1. EDA.ipynb : This jupyter notebook takes in the raw csv files containing
                info about image labels, blacklisted images and outputs two
                pickle objects containing training and testing images' names
                and labels.

                INPUT : Make sure you have the following Folder structure and files
                1. ../data/Data_Entry_2017.csv
                2. ../data/BBox_List_2017.csv
                3. ../data/blacklist_non_PA_AP_view.csv
                4. ../data/blacklist_rotated_images.csv
                5. ../data/blacklist_other_images_with_lower_quality.csv
                6. ../data/train_val_list.txt
                7. ../data/test_list.txt

                OUTPUT:
                1. train_val_filtered.pkl
                2. test_filtered.pkl


2. torch_V100_423.py : The main training file. The code is written in Pytorch and
                assuumes availability of GPU and cuda().

                INPUT:
                1. imagepath = '../data/images/' : Make sure you have all your
                                X-ray images in this folder structure
                2. densenet_model.pkl file*
                3. train_val_filtered.pkl
                4. test_filtered.pkl : Both this files were generated by the running
                                        EDA.ipynb

                * to generate this file, follow the undermentioned instructions
                model = get_symbol() // Need internet connection for this
                with open('densenet_model.pkl', 'wb') as f:
                    pickle.dump(model, f)

                OUTPUT:
                1. Model_all_50_4-23-18.model : The trained model
                2. valid_loss_all_50_4-23-18.csv : CSV files with losses at each
                    epoch saved

3. Trying_CAM_final.ipynb : The file takes the trained model and performs CAM
                    localization on a given image

                    INPUT:
                    1. Model_65_XX_XX-XX_XX.model* : The trained model generated by
                        torch_V100_423.py
                    2. path = "images/"
                    3. images/train_val_filtered.pkl
                    4. images/test_filtered.pkl
                    5. All images in images/

                    OUTPUT:
                    1. CAM.jpg : a localized image
                    2. test.jpg : saves the randomly selected image

                    * Make sure the name matches the output model's name of
                        torch_V100_423.py

4. out_preds.py: Reads the test images and outputs prediction probabilities and
                    labels in csv format (Used to plot ROC curves)

                    INPUT:
                    1. ../data/images/ : ALl images go here
                    2. train_val_filtered.pkl
                    3. test_filtered.pkl
                    4. Model_65_XX_XX-XX_XX.model

                    OUTPUT:
                    1. out_preds.csv: predictions for test images
                    2. out_gt.csv: labels for test images

5. plot_ROC_curve.ipynb: Given predictions and true labels, plots ROC curve

                    INPUT:
                    1. out_preds.csv
                    2. out_gt.csv

                    OUTPUT:
                    1. Inline plot of ROC curve for all diseases


6. api.py : It renders the index.html file in the templates/ folder

            RUN : python api.py

            INPUT:
            1. Model_65_XX_XX-XX_XX.model
            2. templates/index.html



7. Team32ChestXRayPPT.ppsx: recorded and narrated ppt

8. Team32ChestXRayPPT.pdf : Final report
