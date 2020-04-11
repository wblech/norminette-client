#################
# Stage: ruby
FROM ruby:2.7.1-alpine3.11 as ruby
LABEL description="Base ruby image used by other stages"

#################
# Stage: git
FROM alpine as git
LABEL description="Install git and clone norminette repository"

# RUN apk --update add git less openssh && \
# 	rm -rf /var/lib/apt/lists/* && \
# 	rm /var/cache/apk/*

RUN apk --update add git && \
	rm -rf /var/lib/apt/lists/* && \
	rm /var/cache/apk/*

RUN git clone -b feature/actions https://github.com/wblech/norminette-client /home/norminette/

#################
# Stage: bundler
FROM ruby as bundler
LABEL description="Install and cache gems for all environments"

# Copy the Gemfile and Gemfile.lock
COPY --from=git /home/norminette /home/norminette

WORKDIR /home/norminette

RUN bundle

# COPY main .

# RUN ./main

# ENTRYPOINT ["./entrypoint.sh"]

# #################
# # Stage: runner
# FROM ruby as runner

# # Copy bundle config from bundler stage
# # COPY --from=bundler /usr/local/bundle/config /usr/local/bundle/config
# # COPY --from=bundler /home/gems /home/gems
# # Copy norminette folder
# COPY --from=git /home/.norminette /home/.norminette

# WORKDIR /home/.norminette

# RUN gem update --system

# ENTRYPOINT [ "./norminette.rb" ]
