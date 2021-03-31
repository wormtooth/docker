ARG PYTHON_VERSION=3.8
FROM python:${PYTHON_VERSION}

USER root

# install related packages
RUN apt-get update \
	&& apt-get install -yq --no-install-recommends \
	pandoc \
	texlive-xetex \
	texlive-fonts-recommended \
	texlive-generic-recommended \
	nodejs \
	libproj-dev proj-data proj-bin libgeos-dev gdal-bin

# install python packages and build extensions
RUN pip install -U pip wheel setuptools

RUN pip install \
	jupyterlab \
	requests \
	beautifulsoup4 \
	lxml \
	Pillow \
	opencv-python \
	wordcloud \
	Cython \
	sympy \
	numpy \
	pandas \
	matplotlib \
	statsmodels \
	scipy \
	scikit-learn \
	scikit-image \
	jupyter-dash \
	jupyter-server-proxy \
	&& jupyter lab build

# install cartopy
RUN pip install \
	cartopy pyepsg fiona pykdtree OWSLib
RUN pip uninstall -y shapely &&\
    pip install shapely --no-binary shapely

# install pytorch
RUN pip install torch==1.7.0+cpu torchvision==0.8.1+cpu torchaudio==0.7.0 \
    -f https://download.pytorch.org/whl/torch_stable.html

# install sqlalchemy + mysql
RUN pip install SQLAlchemy mysqlclient

# install extra packages
RUN pip install gensim python-dotenv jieba

# install 

ARG USER=jupyter
ARG UID=1000
ARG GID=1000

RUN useradd -m ${USER} --uid=${UID}

USER ${UID}:${GID}

WORKDIR /home/${USER}/notebooks

# Import matplotlib the first time to build the font cache.
ENV XDG_CACHE_HOME="/home/${USER}/.cache/"

RUN MPLBACKEND=Agg python -c "import matplotlib.pyplot"

# Configurate jupyter notebook
# default password: jupyter
ENV PWD_HASH="sha1:cf3676de7ab9:35a0b327a51dcd27e4f83b5ef9545878372e7f94"

RUN mkdir -p /home/${USER}/.jupyter \
&& echo "import os\n\n\
c.NotebookApp.password = os.environ['PWD_HASH']\n\
c.NotebookApp.open_browser = False\n\
c.NotebookApp.ip = '*'\n\
c.NotebookApp.allow_root = True" > /home/${USER}/.jupyter/jupyter_notebook_config.py

VOLUME ["/home/${USER}/notebooks", "/data"]

EXPOSE 8888

ENTRYPOINT ["jupyter", "lab"]
