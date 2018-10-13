
FROM jupyter/minimal-notebook:1145fb1198b2

USER ${NB_USER}

ENV NB_USER jovyan
ENV NB_UID 1000
ENV HOME /home/${NB_USER}

# Make sure the contents of our repo are in ${HOME}

COPY . ${HOME}
USER root
RUN chown -R ${NB_UID} ${HOME}
USER ${NB_USER}

COPY binder/environment.yml ${HOME}

RUN conda env create -f ${HOME}/environment.yml
RUN conda clean --all

RUN source activate research

# Specify the default command to run
CMD ["jupyter", "notebook", "--ip", "0.0.0.0"]
