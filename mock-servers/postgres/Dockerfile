FROM postgres:13

# Create directory for your application
RUN mkdir /tmp/extension
WORKDIR /tmp/extension

# Install Python and the tools needed to handle Python environments
RUN apt-get update && \
    apt-get -y install python3 python3-pip postgresql-plpython3-13 make python3-venv

# Setup the virtual environment
RUN python3 -m venv /venv

# Activate the virtual environment by setting environment variables
ENV PATH="/venv/bin:$PATH"

# Now use pip to install packages in the activated virtual environment
RUN pip install --upgrade pip
RUN pip install boto3

# Copy your SQL scripts, control files, and Makefile
COPY aws_s3--0.0.1.sql aws_s3.control Makefile ./

# Execute the Makefile which likely compiles or configures your PostgreSQL extension
RUN make install
