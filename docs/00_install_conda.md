# 00. Conda/Mamba 설치 가이드


이 문서는 **Linux/WSL/ macOS/ Windows**에서 Miniconda(또는 Mambaforge) 설치와 기본 설정을 다룹니다.
학습/실습을 위해서는 **mamba**를 함께 사용하는 것을 권장합니다(빠른 의존성 해석).

## 1) 선택지 요약
- **Miniconda + mamba 설치** (권장)
- 또는 **Mambaforge**(conda-forge 기본 채널 + mamba 포함 배포)


> 이미 conda를 사용 중이라면 `mamba`만 추가 설치해도 됩니다.


---


## 2) Linux / WSL (Ubuntu 등)
```bash
# (A) Miniconda 설치
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O miniconda.sh
bash miniconda.sh -b -p $HOME/miniconda
$HOME/miniconda/bin/conda init bash
source ~/.bashrc


# mamba 추가 설치 (base)
conda install -n base -c conda-forge mamba -y


# 기본 설정(권장)
conda config --set channel_priority strict
conda config --add channels conda-forge
conda config --show channels

## 3) macOS (Intel/Apple Silicon)
# (A) Miniconda (Intel)
curl -L https://repo.anaconda.com/miniconda/Miniconda3-latest-MacOSX-x86_64.sh -o miniconda.sh
bash miniconda.sh -b -p $HOME/miniconda
$HOME/miniconda/bin/conda init zsh
source ~/.zshrc


# (A) Miniconda (Apple Silicon)
curl -L https://repo.anaconda.com/miniconda/Miniconda3-latest-MacOSX-arm64.sh -o miniconda.sh
bash miniconda.sh -b -p $HOME/miniconda
$HOME/miniconda/bin/conda init zsh
source ~/.zshrc


# mamba 설치
conda install -n base -c conda-forge mamba -y


# 채널/우선순위 설정
conda config --set channel_priority strict
conda config --add channels conda-forge


# (B) 대안: Mambaforge (mamba 포함)
# wget https://github.com/conda-forge/miniforge/releases/latest/download/Mambaforge-Linux-x86_64.sh -O mambaforge.sh
# bash mambaforge.sh -b -p $HOME/mambaforge
# $HOME/mambaforge/bin/conda init bash

## 4) Windows (PowerShell)
# Miniconda 설치 프로그램 다운로드 후 GUI로 설치
# 설치 후 'Anaconda Prompt' 또는 'Miniconda Prompt'에서 다음 실행
conda init
conda install -n base -c conda-forge mamba -y
conda config --set channel_priority strict
conda config --add channels conda-forge

## 5) 설치 확인

conda --version
mamba --version
conda info

6) 자주 나는 이슈

**권한 문제: 홈 디렉토리에 설치, -b(batch) 옵션 사용 권장**

**충돌/의존성 지연: mamba 사용, 채널 우선순위 strict 설정**

**다중 쉘: conda init <shell> 후 쉘 재시작/source 필요**

이 문서는 WGS 마이크로바이옴 분석의 큰 흐름을 설명합니다.


1) **QC**: FastQC, MultiQC, fastp로 리드 품질/어댑터/저품질 제거
2) **Host DNA 제거**: BWA-MEM2/Bowtie2로 hg38 매핑 후 human read 제거
3) **오염 확인**: blank control + Squeegee/Recentrifuge
4) **Taxonomic Profiling**: MetaPhlAn4, Kraken2+Bracken, mOTUs3 교차검증
5) **Functional Profiling**: HUMAnN3/4 (gene family→pathway)
6) **(선택) Assembly/MAG**: MEGAHIT→MetaBAT2→CheckM→GTDB-Tk
7) **통계/시각화**: ANCOM-BC2/ALDEx2/MaAsLin2, Aitchison 거리, PCoA 등
8) **재현성/DB 버전**: conda env, DB 버전 고정, 로그/리포트 관리
