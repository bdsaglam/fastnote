# Hydra

Python library for application configuration 
https://hydra.cc/docs

Usage in Python script
```py
@hydra.main(config_path=str(Path(__file__).parent.parent / "conf"), config_name="config")
def app(cfg : DictConfig) -> None:
    pass

if __name__ == "__main__":
    app()

```

Usage in Jupyter notebook

```py
from hydra import initialize, compose

def load_config(config_path):
    with initialize(config_path=str(config_path)):
        # config is relative to a module
        cfg = compose(config_name="config")
        return cfg
    
cfg = load_config()

```

Overriding default Hydra working directory

```sh
python app.py hydra.run.dir=output/experiment-1
```