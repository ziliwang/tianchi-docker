# python 3.8 cuda 11.1
FROM alpine:3.14

RUN echo http://mirrors.aliyun.com/alpine/v3.10/main > /etc/apk/repositories; \
    echo http://mirrors.aliyun.com/alpine/v3.10/community >> /etc/apk/repositories && \
    # tools
    apk add --no-cache --virtual=.build-dependencies curl bash libstdc++ bzip2 unzip glib libxext libxrender wget && \
    # conda depends
    wget -q -O /etc/apk/keys/sgerrand.rsa.pub https://alpine-pkgs.sgerrand.com/sgerrand.rsa.pub && \
    wget -q -O glibc.apk https://github.com/sgerrand/alpine-pkg-glibc/releases/download/2.23-r3/glibc-2.23-r3.apk && \
    wget -q -O glibc-bin.apk https://github.com/sgerrand/alpine-pkg-glibc/releases/download/2.23-r3/glibc-bin-2.23-r3.apk && \
    apk add *.apk && /usr/glibc-compat/sbin/ldconfig /lib /usr/glibc/usr/lib && \
    # minconda
    export CONDA_DIR=/opt/conda && mkdir -p "$CONDA_DIR" && \
    wget "https://mirrors.tuna.tsinghua.edu.cn/anaconda/miniconda/Miniconda3-py38_4.9.2-Linux-x86_64.sh" -O miniconda.sh -q && \
    bash miniconda.sh -f -b -p "$CONDA_DIR" && export PATH=$CONDA_DIR/bin:$PATH && \
    # minconda set
    # qinghua source
    conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main && \
    conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free && \
    # pytorch
    conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/pytorch/ && \
    # conda-forge
    conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/conda-forge/ && \
    # msys2
    conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/msys2/ && \
    # menpo
    conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/menpo && \
    # others
    conda config --set show_channel_urls yes && \
    conda config --set remote_read_timeout_secs 600.0 && \
    # conda 只对缺失包进行安装，不更新已安装包
    conda update --all --yes && \
    conda config --set auto_update_conda False && \
    # install pytorch cuda
    conda install pytorch torchvision torchaudio cudatoolkit=10.2 -c pytorch && \
    # mechine learning package
    conda install numpy scipy pandas scikit-learn nltk && \
    # other package
    conda install joblib tqdm pyyaml click -y && \
    # install transformer frame
    pip install transformers sentencepiece && \
    # clean conda
    conda clean -tipsy && \
    rm -r "$CONDA_DIR/pkgs/" && \
    mkdir -p "$CONDA_DIR/locks" && \
    chmod 777 "$CONDA_DIR/locks" && \
    # clean pip
    rm -r /root/.cache && \
    # clean lib
    apk del --purge .build-dependencies && \
    # clean tmp
    rm *.apk miniconda.sh

ENV PATH=/opt/conda/bin:$PATH LANG="en_US.utf8" LANGUAGE="en_US:en"