FROM jekyll/jekyll

RUN mkdir /Library

ADD Fonts /Library
ADD Images /Library
ADD blockdiagrc ~/.blockdiagrc

RUN apk add python3 python3-dev jpeg-dev
RUN pip3 install --upgrade pip
RUN pip3 install blockdiag nwdiag
