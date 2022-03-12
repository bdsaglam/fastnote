
## wandb (Weights and Biases)

### Experiment tracking
https://docs.wandb.ai/guides/integrations/fastai

- within a Kaggle notebook
    - define a secret in kernel with `wandb-key` and wandb token
    - login as
```py
import wandb
from kaggle_secrets import UserSecretsClient
user_secrets = UserSecretsClient() 

personal_key_for_api = user_secrets.get_secret("wandb-key")

! wandb login $personal_key_for_api
```

### Loading an artifact
```py
run = wandb.init(project="di504", entity="bdsaglam")
artifact = run.use_artifact('bdsaglam/di504/run-1rub7bk8-model:v1', type='model')
artifact_dir = artifact.download()
```