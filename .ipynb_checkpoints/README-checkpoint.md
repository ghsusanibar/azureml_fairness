<!-- #region -->
# Fairness on Machine Learning

## Overview
As Data Scientist we usually develop analytics models to predict our clients' behaviors such as who are more likely to buy a new product or who are going to cancel their subscription. Analytics models are also designed to distinguish one group from the rest and prioritize them, such as who to approve a loan and who to reject. It is here that special care must be taken because it is possible to have models that in some way discriminate or favor a group of people based on sensitive variables such as sex, race or location. Moreover, many times data scientists seek to have models with the best metrics, high precision or accuracy, but behind it, it may be inducing discrimination just by having the highest metrics in model training. That is why it is very important to have tools that allow us to visualize if this kind of situation is occurring at the moment we train an analytics model. Fairlearn is an open source machine learning toolkit that allow us to build fairer and more inclusive machine learning models. We know that Artificial Intelligence is a field that is going to be more present on our lives and thus it will have a broad impact on society, however it use has to be fair. We have to ensure that all analytics models we develop treat everyone fairly.

![overview](/image/img000.jpg)

## Example of unfair model
For this example I used the Census Dataset in order to train a classification algorithm with the purpose of predict whether a person will be qualified for a loan or not. The dataset has variables related to person information like age, workclass, capital gain but also demographic variables like sex and race. Then I trained a Logistic Regression algorithm for the classification problem and I got an AUC metric of 0.88, which we can say that is a good model. However when I used the Fairness tool, it showed a dashboard in which we can see that there is a disparity in accuracy between women and men and also a difference in how the model made mistakes. 

![example](/image/img008.jpg)

Comparing the false negative rates across the tow different sexes we see that there is more underprediction for the men group than the women group. And for overprediction, the rate is higher for men than women. Additionally, there is a disparity in prediction or disparity in selection rate between the two group of sexes. 

![example](/image/img009.jpg)

From predictions we can see thar 22% of men have got approved for the loan, whereas on woman the ratio is only 7%. We can see that the model has treated different groups of people based on its sex, beaing men group the most benefited for this model. Thus if we deploy this model to production, we'll have a problem for discrimination.

## Use of Fairlearn tool to mitigate disparity
In order to solve this problem we can use the Fairlearn's motigation algorithm (Gridsearh) to mitigate this particular unfairness. The main idea behind this algorithm is treat the fair classification to a sequence of cost-sensitive classification problems. Basically, it trains several models based on the same classification algorithm but with different hyperparameters. The objetive is reduce the dispatity ratio between a specific variable, which in this case is sex. After apply this mitigation algorithm, we can launch other dashboard. We can see in this model comparison chart the accuracy of different models with respect to their disparity in predictions or selection rate. 

![fairlearn](/image/img001.jpg)

So we can choose a model with lower accuracy but with lower disparity in selection rate. The initial model had an AUC metric of 0.88 but 15% of difference on the selection rate between men and women. But if we choose the model with an AUC metric of 0.77, we are going to see that this disparity ratio is reduced to 0.9%, a significant improvement!

![fairlearn](/image/img010.jpg)

So it will depend on how much sacrifice we can make on the accuracy of the model in order to get lower disparity in selection rate. We can decide what model is more appropiate to move forward and deploy it to production. 

## Fairness on AzureML
We can leverage the advantages of the Fairness package on AzureML. In fact, Azure has implemented this Fairness view inside the Azure ML Sutdio. 

![azureml](/image/img006.jpg)

In order to test Fariness preview on Azure ML Studio, I trained differents models with the same dataset. I Trained a Logistic Regression, a Support Vector Machine, a Decision Tree, a Random Forest, a Gradient Boosting, a XGBoost and a LightGBM model. 

![azureml](/image/img007.jpg)
![azureml](/image/img004.jpg)

We can see that all models have similar AUC metric, being LightGBM the model with the hightes metric. However when we inspect the Fairness dashboard we can apreciate that there is differences on the disparity selection ratio between men and women. In fact, the LightGBM model has the hightest AUC metric but also the hightest disparity ratio. So if we only had focused on having a model with the highest metric, we would have had a clear discrimination problem. Therefore the vital importance of having a tool that helps us to visualize and mitigate unfairness at the moment we train an analytics model. Then we can register the models on Azure ML and upload the Fairness dashbord into the Azure ML Studio and interact with others tools that it has.


## Conclusions and Further steps
When we train analytical models many times we only focus on seeking for the model with the highest metric. However we have seen that this can induce problems such as unfairness. Therefore, we can use tools such as Fairness that allow us not only to visualize this effect but also to mitigate it. So when we're about to deploy a model to production, let's make sure it treats all people fairly.

![azureml](/image/img002.jpg)

Additionally, Microsoft has developed six AI principles for Responsible AI. Microsoft is collaborating with researchers and academics around the globe in an effort to advance responsible AI practices and technologies. The AI principles are the following: Fairness (AI systems should treat all people fairly), Reliability & Safety (AI systems should perform reliably and safely), Privacy & Security (AI systems should be secure and respect privacy), Inclusiveness (AI systems should empower everyone and engage people), Transparency (AI systems should be understandable) and Accountability (People should be accountable for AI systems). So as the world increasingly adopts the use of Artificial Intelligence, it will have a greater impact on society, so we must be very responsible in the use we give it. I believe that by following these six AI principles we will be able to develop complete systems that help people in the best way possible.

![azureml](/image/img011.jpg)

## Sources
https://www.microsoft.com/en-us/ai/responsible-ai
https://www.youtube.com/watch?v=Ts6tB2p97ek&ab_channel=MicrosoftDeveloper
https://github.com/fairlearn/fairlearn
https://docs.microsoft.com/en-us/azure/machine-learning/how-to-machine-learning-fairness-aml
https://arxiv.org/pdf/1803.02453.pdf
<!-- #endregion -->
