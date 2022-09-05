FROM python:3.6-slim-buster

# Install OpenCV
# RUN ["apt-get", "install", "-y", "libsm6", "libxext6", "libxrender-dev"]
RUN apt-get update
RUN apt-get install -y build-essential libglib2.0-0 libsm6 libxext6 libxrender-dev
RUN pip3 install opencv-python

# Install dependencies
ADD ./requirements.txt /tmp/requirements.txt
RUN pip3 install --no-cache-dir -q -r /tmp/requirements.txt
# Install torch==1.5.0+cpu, torchvision==0.6.0+cpu
RUN pip3 install torch==1.5.0+cpu torchvision==0.6.0+cpu -f https://download.pytorch.org/whl/torch_stable.html

# Add our code
ADD ./ /opt/app/
WORKDIR /opt/app

# Expose is NOT supported by Heroku
# EXPOSE 5000 

# Run the app.  
# CMD is required to run on Heroku
# $PORT is set by Heroku			
CMD gunicorn --bind 0.0.0.0:$PORT wsgi 