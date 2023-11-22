# Amazon Bedrock Workshop

This hands-on workshop, aimed at developers and solution builders, introduces how to leverage foundation models (FMs) through [Amazon Bedrock](https://aws.amazon.com/bedrock/).

Amazon Bedrock is a fully managed service that provides access to FMs from third-party providers and Amazon; available via an API. With Bedrock, you can choose from a variety of models to find the one that’s best suited for your use case.

Within this series of labs, you'll explore some of the most common usage patterns we are seeing with our customers for Generative AI. We will show techniques for generating text and images, creating value for organizations by improving productivity. This is achieved by leveraging foundation models to help in composing emails, summarizing text, answering questions, building chatbots, and creating images. You will gain hands-on experience implementing these patterns via Bedrock APIs and SDKs, as well as open-source software like [LangChain](https://python.langchain.com/docs/get_started/introduction) and [FAISS](https://faiss.ai/index.html).

Day 1 - Agenda:
1. 10 to 10.30 am - Intro & Voice of customer [30 mins]
2. 10.30 to 11 am – AWS GenAI Overview [30 mins]
3. 11 to 11.30 am - Text Generation [30 mins]
4. 11.30 to 12.00 pm - Text Summarization [30 mins]
5. 12.00 to 1 pm – Lunch
6. 1.00 to 1.45 pm - Questions Answering (RAG) [45 mins]
7. 1.45 to 2.15 pm - Chatbot (RAG) [30 mins]
7. 2.15 to 2.30 pm - EntityExtraction [30 mins]
8. 2.30 to 2.45 pm - Break [15 mins]
9. 2.45 to 3.15 pm - Code Generation [30 mins]
10. 3.15 to 3.45 pm - Chatbot Guardrails [30 mins]


Day 2 - Agenda:
1. 10 to 10.30 am – Recap of Day 1
2. 10.30 to 11 am - Semantic Search with Metadata Filtering [30min]
3. 11.00 to 11.30 am - Semantic Search with Document Summaries [30min]
4. 11.30 to 12 pm – Semantic Search with Re-Ranking [30min]
5. 12 to 1 pm - Lunch
6. 1 to 2.00 pm - Bedrock Agents [60min]
7. 2.00 to 2.30 pm - Wrap up and Next steps


The above agenda is based on selected labs from the following two workshops:
- https://github.com/aws-samples/amazon-bedrock-workshop/
- https://github.com/aws-samples/amazon-bedrock-rag-workshop
For further details on the labs, please refer to the above repositories. 


## Getting started

### self-guided / personal AWS account
#### Choose a notebook environment

This workshop is presented as a series of **Python notebooks**, which you can run from the environment of your choice:

- For a fully-managed environment with rich AI/ML features, we'd recommend using [SageMaker Studio](https://aws.amazon.com/sagemaker/studio/). To get started quickly, you can refer to the [instructions for domain quick setup](https://docs.aws.amazon.com/sagemaker/latest/dg/onboard-quick-start.html).
- For a fully-managed but more basic experience, you could instead [create a SageMaker Notebook Instance](https://docs.aws.amazon.com/sagemaker/latest/dg/howitworks-create-ws.html).
- If you prefer to use your existing (local or other) notebook environment, make sure it has [credentials for calling AWS](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-configure.html).
- To deploy a Amazon SageMaker Domain along with the source code of this repository, log into your AWS Managagement Console and launch the CloudFormation stack below.
<br>
[![Launch CloudFormation Stack](https://felixh-github.s3.amazonaws.com/misc_public/launchstack.png)](https://console.aws.amazon.com/cloudformation/home#/stacks/new?stackName=bedrockworkshop&templateURL=https://felixh-github.s3.amazonaws.com/misc_public/LLMevaluation.yml)

#### Enable AWS IAM permissions for Bedrock

The AWS identity you assume from your notebook environment (which is the [*Studio/notebook Execution Role*](https://docs.aws.amazon.com/sagemaker/latest/dg/sagemaker-roles.html) from SageMaker, or could be a role or IAM User for self-managed notebooks), must have sufficient [AWS IAM permissions](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies.html) to call the Amazon Bedrock service.

To grant Bedrock access to your identity, you can:

- Open the [AWS IAM Console](https://us-east-1.console.aws.amazon.com/iam/home?#)
- Find your [Role](https://us-east-1.console.aws.amazon.com/iamv2/home?#/roles) (if using SageMaker or otherwise assuming an IAM Role), or else [User](https://us-east-1.console.aws.amazon.com/iamv2/home?#/users)
- Select *Add Permissions > Create Inline Policy* to attach new inline permissions, open the *JSON* editor and paste in the below example policy:

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "BedrockFullAccess",
            "Effect": "Allow",
            "Action": ["bedrock:*"],
            "Resource": "*"
        }
    ]
}
```

> ⚠️ **Note:** With Amazon SageMaker, your notebook execution role will typically be *separate* from the user or role that you log in to the AWS Console with. If you'd like to explore the AWS Console for Amazon Bedrock, you'll need to grant permissions to your Console user/role too.

For more information on the fine-grained action and resource permissions in Bedrock, check out the Bedrock Developer Guide.

#### Enable LLMs in Bedrock console
> ℹ️ **Note:** In Within the Amazon Bedrock console, ensure you have agreed to the terms and conditions and enabled the respective LLMs.

#### Clone and use the notebooks

> ℹ️ **Note:** In SageMaker Studio, you can open a "System Terminal" to run these commands by clicking *File > New > Terminal*

Once your notebook environment is set up, clone this workshop repository into it.

```sh
sudo yum install -y unzip
git clone https://github.com/aws-samples/amazon-bedrock-workshop.git
cd amazon-bedrock-workshop
```

You're now ready to explore the lab notebooks! Start with [day1/00_Intro/bedrock_boto3_setup.ipynb]for details on how to install the Bedrock SDKs, create a client, and start calling the APIs from Python.