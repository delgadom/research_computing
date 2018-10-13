
FROM jupyter/base-notebook:1145fb1198b2

ENV NB_USER jovyan
ENV NB_UID 1000
ENV HOME /home/${NB_USER}

RUN adduser --disabled-password \
    --gecos "Default user" \
    --uid ${NB_UID} \
    ${NB_USER}

# Make sure the contents of our repo are in ${HOME}
COPY . ${HOME}
USER root
RUN chown -R ${NB_UID} ${HOME}
USER ${NB_USER}

COPY binder/environment.yml ${HOME}

RUN conda install -y -f ${HOME}/environment.yml

RUN /opt/conda/bin/jupyter serverextension enable --py nbserverproxy --sys-prefix
RUN /opt/conda/bin/jupyter labextension install @jupyter-widgets/jupyterlab-manager \
                             @jupyterlab/hub-extension \
                             @pyviz/jupyterlab_pyviz \
                             jupyter-leaflet \
                             dask-labextension

# Specify the default command to run
CMD ["jupyter", "notebook", "--ip", "0.0.0.0"]
