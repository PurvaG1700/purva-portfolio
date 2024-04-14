---
title: From Brainwave to Machine Learning Grave💀 - Challenges Faced by ML (Machine Learning) Models from Idea to Production. (Deployment Phase)
summary: According to VentureBeat, 87% of data science projects never reach production. In this article, I explore the difficulties of transitioning a machine learning idea into a production environment and the common obstacles encountered along the way. I will also discuss potential solutions to these challenges. This article is based on my experience working in ML operations for digital agriculture solutions at Syngenta.

date: 2023-07-27
custom_reading_time: 4
math: true
image:
  placement: 2
  caption: 'Image credit: Syngenta Medium Blog)'
external_link: https://medium.com/syngenta-digitalblog/from-brainwave-to-machine-learning-grave-challenges-faced-by-ml-machine-learning-models-from-dff73d8234f3
---

From Brainwave to Machine Learning Grave💀: Challenges Faced by ML (Machine Learning) Models from Idea to Production. (Deployment Phase)


In the decade of ChatGPT (🤫: who generated the title), we still imagine a world where all ML ideas convert into reality. Building an ML model that solves a real-world problem is enticing. In a parallel universe, you create a model, train it on a massive dataset, and validate it with remarkable accuracy; boom, you have a system that solves the intended problem. But the reality is far from this dream. According to VentureBeat, 87% of data science projects never make it into production. According to Algorithmia, 64% of organizations spend a month or longer to deploy a model.

In this article, we will explore the challenges faced while converting an ML idea to production and the pain points of the journey. A more comprehensive list is presented in the following studies “Challenges in Deploying Machine Learning: A Survey of Case Studies, Paleyes et al., Jan 2021” and “Hidden Technical Debt In Machine Learning Systems, Sculley et al., Dec 2015.”


ML model deployment:

After we have built a good-performing ML model (sleepless nights 💤), the next step is to deploy the ML model for consumption. ML engineering and DevOps play an essential role in the success of an ML model and the deployment phase. This step is challenging, and below are the most common problems faced.

Model integration

Deciding how to integrate the model to fit into the existing system and be consumed quickly is essential. Multiple options of using FastAPI or using serving tools like Seldon, Kserve, TFServing, etc., is a daunting decision. The key factors are the system’s reusability and how easy it is to onboard new models and alter existing ones.

Sometimes running after technologies over solutions can bring unnecessary problems. While working on integrating and deploying models at Syngenta the team tried to implement Seldon for creating a service on the fly instead of FastAPI. Though there are numerous benefits of Seldon we found that this was not a good fit where we had pure mathematical models, models concerning different pre- and post-processing, and thus working with Seldon became cumbersome to the point that we moved back to FastAPI.

Deployment infrastructure and scalability

As simple as it might sound, a vague understanding of the infrastructure and scalability can impact user trust, model availability, and model reliability. A model may need a specific type of resource for computation, and it is crucial that the underlying infrastructure aids in fulfilling the business requirements. One another factor that affects the scalability of deployment is the model size and performance. Sometimes model packages may be a complete black box, and a lot of glue code gets generated to manage discrete packages and processing. Glue code often reduces the performance of the deployed API (Application Programming Interface). A nasty ML code can decrease agility over time and lead to redoing the entire architecture.

Full-fledged technologies like Kubeflow and AWS (Amazon Web Services) SageMaker present a collection of tools to help the lifecycle of ML models from development to production-grade deployment. Such tools and platforms can also help data scientists to deploy ML models to production with straightforward steps, even without extensive knowledge of technologies like Kubernetes. The mentioned technologies manage the infrastructure, and you only need to worry about the code.

While deploying an ML model concerning imagery, my team at Syngenta encountered a problem concerning model performance. The guidelines for scalability were not clear. The team worked on deploying the model and later found that the expectation for the number of requests per second was more than predicted. Even though autoscaling is a thing, the model depends on numerous factors and database connections and queuing mechanisms. We need to look out for such things in the preliminary stages to avoid unnecessary re-work. Such problems can be dealt with simply by increasing the number of maxPods in your deployment, but sometimes it causes a lot of fire on the slack/teams channels🔥🚒🧯

Model monitoring and updates

Once the model gets deployed for consumption, monitoring for performance, health, and accuracy is important. With time the models may degrade with new data coming into the system. Such degradation in performance calls for retraining the models. One must have proper monitoring, health checks, notifications, and alerts for the deployment.

We often think the first model we deploy is the only one we will deploy. At Syngenta, we prioritize incremental changes in models over including everything at once. This makes sure we do not have breaking changes and helps us to check the impact of changes made.

Configuring CICD for testing, validating, and deploying new models can aid in faster time to production. A properly configured CICD will also reduce the chance of piling unreleased changes. In some cases, a subsequent release often refers to a breaking change that alters the entire system. The previous work is a waste in such cases. A feedback loop is essential for updating the model and tuning the parameters. Implementing a feedback loop correctly to ensure the user does not report erroneous data is also challenging.

Many tools are present out there to get logs, traces, and alerts for your deployed services. Often choosing the right tool can be a lot of PoC (proof of concept) work, but it is worth the investment. At Syngenta, we used a tool to get traces for our services, but the tool was not working well enough for detecting logs and correlating them to respective traces. It caused a lot of inconvenience to get insights about the deployed services. We use Datadog for Application Performance Monitoring; it is easier to configure and provides great visibility. Choosing the right tool that fits your infrastructure and needs is crucial and will help eventually. Proper monitoring and alerts also help with the visibility of your service health.

Differences in training and serving pipelines

One of the classic problems is the difference in the training and serving pipeline. You may get the desired metrics while training the model, but the difference in data, implementation, versioning, and dependencies in the serving phase can produce the wrong output. In agriculture, most models will depend on the weather, and the unpredictability of data affects the model performance.

When you design a model specifically for batch processing and suddenly want it to handle real-time online requests, it may be a huge challenge to feed data to the model and do the correct preprocessing.

The addition of synthetic data and data for predictable scenarios that may occur and are not present currently are ways to make your model handle a wide range of requests accurately. Implementing feature stores, versioning tools, and A/B testing can help reduce the gap and ensure a peaceful Friday night after the production release.

Poor connection between the research and deployment team

For example, Alex from the ML engineering team assumed that the predicted crop yield by the yield prediction model is in kg/ha, but it is bushels/acre. Though this might be a quick fix, some problems cause delays in deployment, unsatisfied business requirements, friction between teams, and even rewriting a piece of logic that packaged model already handles. It is a common suggestion that engineering and research teams work together rather than in isolated environments and often can be the same team with two roles.

It is also essential to confirm the effects of wrong predictions, false negatives, and false positives with the stakeholders. A false negative can be worse than a false positive. E.g., sometimes the model may be working on a critical aspect such as breast cancer detection, and a false negative can be a disastrous situation.

Long story short:

These are some general problems faced by most of the teams which may sound very trivial but will cause a lot of technical debt. Make sure you keep an eye on these crucial points and tackle them at an early stage. There might be many such problems organizations and individuals face on a day-to-day basis while deploying ML models. If you are facing a unique issue, please feel free to comment; if you have already tackled it, please mention it in the comments section. Cheers!! 🥂