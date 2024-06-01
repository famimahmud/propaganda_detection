# propaganda_detection
 
 This is our repository for [SemEval 2024 Challenge](https://propaganda.math.unipd.it/semeval2024task4/index.html). We implemented subtask 1, 2A and 2B of the challenge. Solutions and trained models for each tasks can be found in their respective directories.

 Our report is [here](https://gitlab.lrz.de/masters-thesis-daryna/nlp-lab-ws2023/persuasion_technique_detection/-/blob/main/Detection_of_Persuasion_Techniques_in_Memes_Report.pdf) and our poster is [here](https://gitlab.lrz.de/masters-thesis-daryna/nlp-lab-ws2023/persuasion_technique_detection/-/blob/main/Poster_Detection_of_Persuasion_Techniques_FINAL.pdf?ref_type=heads).

## Datasets
Until the actual test set was published, we had trained our models with train set, validated with validation set and tested our performance on the development set. We were able to submit our development set results on the leaderboard to see our place among other contestants and improve our implementation. We only did one final submission on the test set after finalizing our pipelines.
|    | Train Set | Validation Set | Development Set | Test Set |
|---------|-----|-------------|-------------|-------------|
| Subtask 1   | 7000  | 500  | 1000 | 1500 |
| Subtask 2A  | 7000  | 500  | 1000 | 1500 |
| Subtask 2B | 1200  | 150  | 300 | 600 |

## Subtask 1
The experiments for Subtask 1 can be found in [subtask1](https://gitlab.lrz.de/masters-thesis-daryna/nlp-lab-ws2023/persuasion_technique_detection/-/tree/main/subtask1)

- The final hierarchical pipeline can be run using the notebook:
[treeClassification_s1.ipynb](https://gitlab.lrz.de/masters-thesis-daryna/nlp-lab-ws2023/persuasion_technique_detection/-/blob/main/subtask1/transformer/training/treeClassification_s1.ipynb)
- The multilabel pipeline can be run using the notebook:
[multilabelClassification_s1.ipynb](https://gitlab.lrz.de/masters-thesis-daryna/nlp-lab-ws2023/persuasion_technique_detection/-/blob/main/subtask1/transformer/training/multilabelClassification_s1.ipynb)
- The ensembling with stacking method experiments can be found in:
[ensembling](https://gitlab.lrz.de/masters-thesis-daryna/nlp-lab-ws2023/persuasion_technique_detection/-/tree/main/subtask1/transformer/ensembling)
## Subtask 2B
 For this challenge we used 2 types of models; text transformer([BERTweet-Large](https://arxiv.org/abs/2005.10200)) and an image model(CNN based or a vision transformer). Text transformer processes the text in the meme using the corresponsing json of the given meme while the image model processes the meme. We concatanate the embeddings from these 2 models and pass the concatanated vector to 2 consecutive linear layers for the final classification. We experiemented with different image models, different methods of embedding usage(average of the tokens, pooler_output, CLS), cross attention and stacking as ane ensembling method (linear layers, random forest classifier, logistic regression). We obtained the best development set result using end-to-end training using the average of all token embeddings in [BERTweet-Large](https://arxiv.org/abs/2005.10200) and [google/vit-base-patch32-224-in21k](https://arxiv.org/abs/2010.11929) as image transformer.

- The final pipeline used for the final training and then test set predictions: [subtask2b_AVG_test_predictions.ipynb](https://gitlab.lrz.de/masters-thesis-daryna/nlp-lab-ws2023/persuasion_technique_detection/-/blob/main/subtask2b/subtask2b_AVG_test_predictions.ipynb?ref_type=heads)

The summaries for our experiemnts are stored in these directories: subtask2b/CLS_summaries, subtask2b/pooler_output_summaries, subtask2b/summaries_avg, subtask2b/summaries_crossattention

Our other experiments:
- Using AVG embeddings: [subtask2b-AVG.ipynb](https://gitlab.lrz.de/masters-thesis-daryna/nlp-lab-ws2023/persuasion_technique_detection/-/blob/main/subtask2b/subtask2b-AVG.ipynb)
- Using CLS embeddings: [subtask2b-CLS.ipynb](https://gitlab.lrz.de/masters-thesis-daryna/nlp-lab-ws2023/persuasion_technique_detection/-/blob/main/subtask2b/subtask2b-CLS.ipynb)
- Using pooler_output embeddings: [subtask2b-POOLER_OUTPUT.ipynb](https://gitlab.lrz.de/masters-thesis-daryna/nlp-lab-ws2023/persuasion_technique_detection/-/blob/main/subtask2b/subtask2b-POOLER_OUTPUT.ipynb)
- Stacking method using random forest or logistic regression: [subtask2b-stacking_method.ipynb](https://gitlab.lrz.de/masters-thesis-daryna/nlp-lab-ws2023/persuasion_technique_detection/-/blob/main/subtask2b/subtask2b_stacking_method.ipynb)
- Stacking method with linear layers as meta model: [subtask2b_stacking_method_LinearLayers.ipynb](https://gitlab.lrz.de/masters-thesis-daryna/nlp-lab-ws2023/persuasion_technique_detection/-/blob/main/subtask2b/subtask2b_stacking_method_LinearLayers.ipynb)
- Using only the text model: [subtask2b-text_only.ipynb](https://gitlab.lrz.de/masters-thesis-daryna/nlp-lab-ws2023/persuasion_technique_detection/-/blob/main/subtask2b/subtask2b_text_only.ipynb) 
- Using only the image model: [subtask2b-train_only_image_model.ipynb](https://gitlab.lrz.de/masters-thesis-daryna/nlp-lab-ws2023/persuasion_technique_detection/-/blob/main/subtask2b/subtask2b_train_only_image_model.ipynb) 
- Removing the texts from the memes: [Remove_texts_from_images.ipynb](https://gitlab.lrz.de/masters-thesis-daryna/nlp-lab-ws2023/persuasion_technique_detection/-/blob/main/subtask2b/Remove_texts_from_images.ipynb) 
- Attention maps of the best performing model on the the original dataset and the altered dataset whose texts are removed: [subtask2b_visualize_attention.ipynb](https://gitlab.lrz.de/masters-thesis-daryna/nlp-lab-ws2023/persuasion_technique_detection/-/blob/main/subtask2b/subtask2b_visualize_attention.ipynb)
- Image models we experimented: 
[google/vit-base-patch16-224-in21k](https://arxiv.org/abs/2010.11929), [google/vit-base-patch16-384](https://arxiv.org/abs/2010.11929), [google/vit-base-patch32-224-in21k](https://arxiv.org/abs/2010.11929), [google/vit-base-patch32-384](https://arxiv.org/abs/2010.11929), [openai/clip-vit-base-patch16](https://arxiv.org/abs/2103.00020), [openai/clip-vit-base-patch32](https://arxiv.org/abs/2103.00020), [microsoft/resnet-50](https://arxiv.org/abs/1512.03385), [microsoft/resnet-152](https://arxiv.org/abs/1512.03385), [google/efficientnet-b5](https://arxiv.org/abs/1905.11946)

## Subtask 2A
The Final pipeline for Subtask 2a can be found in [subtask2a](https://gitlab.lrz.de/masters-thesis-daryna/nlp-lab-ws2023/persuasion_technique_detection/-/tree/main/subtask2a?ref_type=heads)
## Team members
- Gözde Ünver
- Fami Mahmud
- Batıkan Özkul
