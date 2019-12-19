# pythonsevilla2019
This repo contains notebooks, code and presentation about the meetup [*Introducción a MLFlow y Databricks: acelerando el Machine Learning Lifecycle*](https://www.meetup.com/Python-Sevilla/events/266430587/) in the meetup group of [Python Sevilla Developers](https://www.meetup.com/Python-Sevilla).

Slides can be found both on [Slideshare](https://www.slideshare.net/fortega86/pythonsevilla2019-mlflow-introduction) and [in this repository](pythonsevilla2019 - Introducción a MLFlow.pdf)

## Installation and use
1. ``pip install -r requirements.txt``
2. ``jupyter notebook``

## MLFlow Tracking demo
Run ``jupyter notebook`` and execute the notebook ``tracking.ipynb``.

To execute the last section is necessary to possess an Azure or AWS account with a deployed Databricks resource.

## MLFlow Projects demo
The first example uses a public project located in the official MLFlow repository (https://github.com/mlflow/)

``mlflow run https://github.com/mlflow/mlflow-example.git -P alpha=5``

The second example uses our own project (./project_example)

```bash
cd project_example
mlflow run . -P n_estimators=500
```

## MLFLOW Models demo
Execute the notebook ``models.ipynb``.

The second part of the demo consist on deploying a trained model from the ``mlruns`` folder that MLFlow creates after tracking experiments.

So, it is necessary to navigate through the corresponding folder and execute the ``mlflow serve`` command.

```bash
cd mlruns/<selected experiment_id>/<selected run_id>/artifacts/model/
mlflow models serve -m . -p 1234
```

After some time, a gunicorn + Flask microservice is deployed on port 1234. It is possible to send http post request by means of programs like Postman. The endpoint is:

``localhost:1234/invocations``

And this is an example of valid body for the request:

```json
{
	"data": [[ 0.52444161,  0.97309661,  0.43247518,  0.38717859, -1.03377319,
       -0.73048166, -0.70972218, -0.41044243, -1.00047971, -0.82507126,
       -0.08818832, -0.04623819, -0.18209319, -0.0038316 , -1.04758402,
       -0.93257644, -0.65865037, -0.69601737, -0.71241416, -0.25530814,
        0.58767599,  1.36061943,  0.48167379,  0.44795641, -0.62887522,
       -0.64418546, -0.62375274, -0.23693879,  0.08147618,  0.05512114]]
}
```