# Visualizing Results

What if you want to share results of flows with human beings or inspect results by yourself? One option is to use Jupyter notebooks and Metaflow [Client API](../client.md), which is a good combination for ad-hoc analysis and exploration.

If you have a good idea what information you want observe in every execution, it is more convenient to produce a relevant report automatically. Metaflow comes with a built-in mechanism to create and view such reports with a few lines of code, called _cards_. These cards can contain any images, text, and tables which help you observe the flow. To get an idea of how cards works in practice, take a look at the following short video (no sound):

{% embed url="https://www.youtube.com/watch?v=YSJXn6KLzXg" %}

## What are cards?

Here are some illustrative use cases that cards are a good fit for:

* Creating a report of model performance or data quality every time a task executes, for instance, every time a new model is trained.
* Sharing human-readable results with non-technical stakeholders.
* Debugging task behavior by attaching a suitable card to the flow during development.
* Experiment tracking: comparing results across multiple runs**.**

In contrast, cards are not meant for building interactive dashboards, monitoring tasks while they are executing, or for ad-hoc exploration that is a spot-on use case for notebooks. If you are curious, you can read more about the motivation for cards in [the original release blog post](https://outerbounds.com/blog/integrating-pythonic-visual-reports-into-ml-pipelines/).

You can attach cards in any Metaflow step. When a task corresponding to the step finishes, an additional piece of code is executed which creates an HTML file visualizing the results of the task. In the illustration below, the train step trains three models in parallel by using [foreach](../basics.md#foreach). The step is decorated with the `@card` decorator, so it produces a human-readable report alongside its usual programmatic results.

![](<../../.gitbook/assets/Visualizing Results (1).png>)

Each model could be accompanied by a card showing model validation metrics. For instance, you can easily customize the cards to look something like this:

![](../../.gitbook/assets/card-docs-roc.png)

Note that cards don’t change the behavior of the workflow in any way. They are created and stored independently from the flow or task. Should something fail during the creation of a card, the execution of the workflow is not affected, which makes cards safe to use even in sensitive production deployments. Also, crucially, cards work in any compute environment such as laptops, [AWS Batch](../scaling.md), or when the flow is scheduled to run automatically e.g. on [AWS Step Functions](../../going-to-production-with-metaflow/scheduling-metaflow-flows.md). Hence, you can use cards to inspect and debug results during prototyping, as well as monitor the quality of production runs.

Currently, there are three main mechanisms for viewing cards, which are discussed in detail below:

1. You can use [the `card view` command](effortless-task-inspection-with-default-cards.md) on the command line to open a card in a local web browser.
2. You can use [the `get_cards` API](effortless-task-inspection-with-default-cards.md#accessing-cards-via-an-api) to access cards programmatically, e.g. in a notebook.
3. If you have [the Metaflow Monitoring GUI](https://netflixtechblog.com/open-sourcing-a-monitoring-gui-for-metaflow-75ff465f0d60) deployed, cards will automatically show in the task page, as shown in the video above.

You can customize the content of cards as much or as little as you want: You can attach a [_Default Card_](effortless-task-inspection-with-default-cards.md) to any existing workflow without changing anything in the code. Or, with a few lines of Python, you can create a card with custom content by using built-in [_Card Components_](easy-custom-reports-with-card-components.md). If you need even more flexibility, you can find or create a [_Card Template_](advanced-shareable-cards-with-card-templates.md) to output a report formatted with arbitrary HTML and Javascript.

Learn more about these approaches in the following subsections:

1. [Effortless Task Inspection with Default Cards](effortless-task-inspection-with-default-cards.md)
2. [Easy Custom Reports with Card Components](easy-custom-reports-with-card-components.md)
3. [Advanced, Shareable Cards with Card Templates](advanced-shareable-cards-with-card-templates.md)

If you are unsure, start with the [_Default Cards_](effortless-task-inspection-with-default-cards.md) which explains the basics of card usage.
