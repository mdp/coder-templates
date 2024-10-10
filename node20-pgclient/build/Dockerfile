FROM ubuntu

RUN apt-get update \
	&& apt-get install -y \
	build-essential \
	curl \
	git \
	golang \
	sudo \
	vim \
	wget \
	libssl-dev \
	libreadline-dev \
	zlib1g-dev \
	libcurl4-openssl-dev \
	uuid-dev \
	icu-devtools \
	libicu-dev \
	&& rm -rf /var/lib/apt/lists/*


ARG USER=coder
RUN useradd --groups sudo -m --shell /bin/bash ${USER} \
	&& echo "${USER} ALL=(ALL) NOPASSWD:ALL" >/etc/sudoers.d/${USER} \
	&& chmod 0440 /etc/sudoers.d/${USER}
USER ${USER}


RUN git clone --depth 1 https://github.com/asdf-vm/asdf.git $HOME/.asdf

RUN echo '. ~/.asdf/asdf.sh' >> ~/.bashrc

# Set up asdf environment
ENV ASDF_DIR=/home/${USER}/.asdf
ENV PATH=$ASDF_DIR/bin:$ASDF_DIR/shims:$PATH

RUN asdf plugin add nodejs && \
    asdf install nodejs latest:20 && \
    asdf global nodejs latest:20

RUN asdf plugin add postgres && \
    asdf install postgres latest:16 && \
    asdf global postgres latest:16


WORKDIR /workspace
