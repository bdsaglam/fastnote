

## correlation heatmap seaborn
```py
corr = df.corr()
sns.heatmap(corr, vmin=-1, vmax=1, cmap=sns.color_palette("vlag", as_cmap=True), square=True)
```

## figures for papers
```py
%matplotlib inline
import matplotlib as mpl

from pathlib import Path
Path('./figures').mkdir(parents=True, exist_ok=True)

plt.rc('font', family='serif')
# plt.rc('text', usetex=True)
mpl.rcParams['figure.dpi'] = 300

def savefig(name, **kwargs):
    params = dict(bbox_inches='tight', transparent="True", pad_inches=0)
    params.update(kwargs)
    plt.savefig(f'./figures/{name}.png', **params)

```