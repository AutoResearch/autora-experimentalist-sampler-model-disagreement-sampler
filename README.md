# AutoRA Model Disagreement Sampler

The model disagreement sampler identifies experimental conditions $\vec{x}' \in X'$ with respect to
a pairwise distance metric between theorist models, $P_{M_{i}}(\hat{y}, \vec{x}')$:

$$
\underset{\vec{x}'}{\arg\max}~(P_{M_{1}}(\hat{y}, \vec{x}') - P_{M_{2}}(\hat{y}, \vec{x}'))^2
$$

# Example Code

```
from autora.experimentalist.sampler.model_disagreement_sampler import model_disagreement_sampler
from autora.theorist.bms import BMSRegressor; BMSRegressor()
from autora.theorist.darts import DARTSRegressor; DARTSRegressor()
import numpy as np

#Meta-Setup
X = np.linspace(start=-3, stop=6, num=10).reshape(-1, 1)
y = (X**2).reshape(-1, 1)
n = 5

#Theorists
bms_theorist = BMSRegressor()
darts_theorist = DARTSRegressor()
bms_theorist.fit(X,y)
darts_theorist.fit(X,y)

#Sampler
X_new = model_disagreement_sampler(X, [bms_theorist, darts_theorist], n)
```