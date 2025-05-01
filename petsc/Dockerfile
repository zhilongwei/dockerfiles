FROM debian:stable

RUN apt-get update && apt-get install -y --no-install-recommends \
		build-essential \
		gfortran \
		python3 \
		git \
		cmake \
		flex \
        ca-certificates && \
	apt-get clean && \
    rm -rf /var/lib/apt/lists/*
		
ENV PETSC_DIR=/petsc
ENV PETSC_ARCH=arch-linux-c-noncomplex-debug

RUN git clone -b release https://gitlab.com/petsc/petsc.git ${PETSC_DIR} &&\
    cd ${PETSC_DIR} &&\
    git pull &&\
    git checkout v3.23.1

RUN cd ${PETSC_DIR} && \
		./configure PETSC_ARCH=${PETSC_ARCH} --with-cc=gcc \
		--with-cxx=g++ \
		--with-fc=gfortran \
		--download-mpich \
		--download-fblaslapack \
		--download-superlu \
		--download-superlu_dist \
		--download-mumps \
		--download-scalapack \
		--download-parmetis \
		--download-metis \
		--download-ptscotch \
		--download-bison \
		--download-eigen \
		--download-hdf5 && \
	make PETSC_DIR=${PETSC_DIR} PETSC_ARCH=${PETSC_ARCH} all && \
	make PETSC_DIR=${PETSC_DIR} PETSC_ARCH=${PETSC_ARCH} check
		