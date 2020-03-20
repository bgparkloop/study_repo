# Jupyter Notebook

### gzip 모듈

gzip 모듈을 이용하면 파일을 저장할 때, 압축하여 저장하여 용량을 절약할 수 있음.

```text
import gzip
import pickle

data = [....]

# 저장 시
with gzip.open(data_path, 'wb') as f:
    pickle.dump(data, f)
    
# 로드 시
with gzip.open(data_path, 'rb') as f:
    data = pickle.load(f)
```

### IPython Widget 사용

* [https://junpyopark.github.io/interactive\_jupyter/](https://junpyopark.github.io/interactive_jupyter/)
* [https://minrk-ipywidgets.readthedocs.io/en/latest/examples/Using%20Interact.html](https://minrk-ipywidgets.readthedocs.io/en/latest/examples/Using%20Interact.html)
* [https://bugsdb.com/\_ko/debug/024925049a58271168f4c4b0bda8a634](https://bugsdb.com/_ko/debug/024925049a58271168f4c4b0bda8a634)

### Python 코드 내 Shell 명령어 사용

* os 모듈 사용

```text
import os

result = os.popen('sha256sum {}'.format(path)).read()
print(result)
```

* subprocess 모듈 사용

```text
import subprocess

result = subprocess.check_output('sha256sum {}'.format(path), shell=True)
print(result)
```



