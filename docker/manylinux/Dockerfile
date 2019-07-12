FROM quay.io/pypa/manylinux2010_x86_64
MAINTAINER Henri Menke <pairinteraction@henrimenke.de>

# Use Python 3.5
ENV PATH="/opt/python/cp35-cp35m/bin/:$PATH"
ENV PYTHON_INCLUDE_DIR="/opt/python/cp35-cp35m/include/python3.5m/"

# We have to install all kinds of things by hand.
#
# From pip:
#     cmake, numpy, scipy
#
# From the official repos:
#     curl, gsl-devel, pcre-devel, boost-devel
#
#     curl and pcre-devel are required to build other packages from
#     source.
#
# From source:
#     swig
#
#     The sources and build directories are deleted after finishing to
#     save space.
#
RUN pip3 install cmake numpy==1.11.0 scipy==0.17.0 \
  && echo 'echo "pyuic5 $@"' > /usr/local/bin/pyuic5 \
  && chmod +x /usr/local/bin/pyuic5 \
  && yum install -y curl gsl-devel pcre-devel boost-devel \
  && curl -LO http://prdownloads.sourceforge.net/swig/swig-3.0.12.tar.gz \
  && tar xzvf swig-3.0.12.tar.gz \
  && cd swig-3.0.12 \
  && ./configure \
  && make \
  && make install \
  && cd .. \
  && rm -rf swig-3.0.12*
