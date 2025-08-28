# pytorch-sparselu-install
## The way of installing PyTorch that enable to use torch.sparse.spsolve()
1. conda 가상환경 생성 (python 버전은 3.13 이상?)
2. conda activate  가상환경
3. conda install numpy pyyaml mkl mkl-include setuptools cmake cffi typing_extensions future six requests 
   conda install cmake=3.26 <== 핵심...
4. conda 가상환경에 cudss 설치: pip install nvidia-cudss-cu12 
5. which nvcc 했을 때 /usr/local/cuda-12.9/bin/nvcc 나오는지 확인
6. pytorch 직접 빌드를 위해 git clone하기: git clone --recursive https://github.com/pytorch/pytorch.git

7. 아래 명령어들 수행
- cd pytorch
- git checkout v2.5.1
- git submodule sync
- git submodule update --init --recursive

8. pytorch/ 안에서
- rm -rf build
- rm -rf dist
- rm -rf *.egg-info

export USE_CUDSS=1
export TORCH_CUDA_ARCH_LIST="8.9"   # GPU 아키텍처 맞게
- pip install -r requirements.txt
- python setup.py bdist_wheel

9. 성공시 pytorch/dist/ 안에 wheel 파일 생성
10. wheel로 conda 가상환경에 pytorch 설치: pip install --force-reinstall "생성된 wheel 파일" 
