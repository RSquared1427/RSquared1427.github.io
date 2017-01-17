---
published: false
---
	git clone https://github.com/dmlc/mxnet

cd mxnet
git submodule update --init --recursive

mkdir build
cd build
module load gcc
module load cmake/3.6.0

cmake -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX:PATH=${HOME}/opt/ -DBLAS=mkl -DINTEL_ROOT=/apps/rhel6/intel/compilers_and_libraries_2016.1.150/linux -DUSE_OPENCV=0 -DUSE_CUDA=0 -DUSE_CUDNN=0 ..

make all -j 8

cd ..
mkdir lib
cp build/libmxnet.so lib/

cd python
python setup.py install --user
cd ..

Rscript -e "install.packages('devtools', repo = 'https://cran.rstudio.com')"
cd R-package
sudo Rscript -e "library(devtools); library(methods); options(repos=c(CRAN='https://cran.rstudio.com')); install_deps(dependencies = TRUE)"
cd ..
make rpkg
R CMD INSTALL mxnet_0.7.tar.gz

