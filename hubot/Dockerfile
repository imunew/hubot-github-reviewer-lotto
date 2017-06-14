FROM node:4.8

RUN npm install -g yo generator-hubot
RUN npm install hubot-slack --save
RUN npm install underscore async github@8.2.1 weighted --save

RUN useradd hubot -m

USER hubot
WORKDIR /home/hubot

# Create hubot
RUN yo hubot --defaults --adapter slack

ADD ./external-scripts.json /home/hubot/external-scripts.json
ADD ./scripts/reviewer-lotto.coffee /home/hubot/scripts/reviewer-lotto.coffee

CMD bin/hubot --adapter slack
