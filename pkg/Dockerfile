#===============================================================================
# FROMFREEZE docker.io/library/debian:10
FROM docker.io/library/debian@sha256:5625c115ad881f19967a9b66416f8d40710bb307ad607d037f8ad8289260f75f

ARG USER=x
ARG HOME=/home/x
#-------------------------------------------------------------------------------
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
        ca-certificates \
        curl && \
    rm -rf /var/lib/apt/lists/*

RUN useradd ${USER} -d ${HOME} && \
    mkdir -p ${HOME}/bin && \
    chown -R ${USER}:${USER} ${HOME}
#-------------------------------------------------------------------------------
COPY bin/ ${HOME}/bin/
#-------------------------------------------------------------------------------
USER ${USER}

WORKDIR ${HOME}

ENV PATH=${HOME}/bin:$PATH \
    LANG=C.UTF-8

CMD ["isx-plug-elasticsearch", "-b", "localhost", "-p", "8000"]

EXPOSE 8000

HEALTHCHECK CMD curl -fs http://localhost:8000 || false
#===============================================================================
