---
title: "Setting up VScode to test python scripts on WSL2 ubuntu"
date: 2020-09-16
categories: python
---

1. WSL2 setup WSL2 설치하기

Basic setup - [official docs][MS-WSL2]


2. Ubuntu apt repo url 변경하기

기본 url에서 kakao mirror로 변경하는 법은 [이 블로그][apt-kakao]를 참고함


3. Ubuntu 설정

[official docs][vscode-wsl2-python]

 - official docs와는 다르게 pip 대신 miniconda로 virtualenv를 만들어 관리하고자 함.
 ```bash
#update
sudo apt update

#miniconda3 python3.8
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
```


 - miniconda base directory는 용량이 큰 D drive 쪽에 설정함 : /mnt/d/linux_miniconda/miniconda3

```bash

#miniconda3 setting
# Do you accept the license terms? [yes|no]
# [no] >>> yes

# Miniconda3 will now be installed into this location:
# /home/hd00ljy/miniconda3

#   - Press ENTER to confirm the location
#   - Press CTRL-C to abort the installation
#   - Or specify a different location below

# [/home/hd00ljy/miniconda3] >>> /mnt/d/linux_miniconda/miniconda3
# PREFIX=/mnt/d/linux_miniconda/miniconda3
```


- conda base env가 자동으로 켜지지 않도록 설정

```bash

conda config --set auto_activate_base false
```

- python virtualenv 만들어 python 및 필요한 툴들 설치

```bash
conda install -c bioconda pysam pybedtools

```




[MS-WSL2]:  https://docs.microsoft.com/ko-kr/windows/wsl/install-win10#update-to-wsl-2
[apt-kakao]: https://teddylee777.github.io/linux/ubuntu%EC%97%90%EC%84%9C-apt-get%EC%98%A4%EB%A5%98%EC%8B%9C-mirror%EC%82%AC%EC%9D%B4%ED%8A%B8-%EC%97%85%EB%8D%B0%EC%9D%B4%ED%8A%B8%EB%B0%A9%EB%B2%95
[vscode-wsl2-python]: https://code.visualstudio.com/docs/remote/wsl-tutorial#_python-development


```python
def print_hi(name):
  print("hello", name)
print_hi('Tom')
```

Check out the [Jekyll docs][jekyll-docs] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll’s GitHub repo][jekyll-gh]. If you have questions, you can ask them on [Jekyll Talk][jekyll-talk].

[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
