FROM pytorch/pytorch:1.9.0-cuda10.2-cudnn7-runtime

RUN export CONDA_DIR=/opt/conda && \
    conda config --set ssl_verify no && \
    # conda update --all --yes && \
    conda config --set auto_update_conda False && \
    # install pytorch cuda
    # conda install pytorch torchvision torchaudio cudatoolkit=10.2 -c pytorch && \
    conda install curl python=3.8 -y && \
    # install transformer frame
    pip install transformers sentencepiece pytorch-crf numpy scipy pandas scikit-learn nltk matplotlib -i https://mirrors.aliyun.com/pypi/simple/ && \
    # clean conda
    conda clean -tipsy && \
    rm -r "$CONDA_DIR/pkgs/" && \
    # mkdir -p "$CONDA_DIR/locks" && \
    # chmod 777 "$CONDA_DIR/locks" && \
    # clean pip
    rm -r /root/.cache

ENV LANG="en_US.utf8" LANGUAGE="en_US:en" CONDA_AUTO_UPDATE_CONDA="false"