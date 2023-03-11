# Use the official Ruby image as the base image
FROM ruby:3.0.5-alpine

# Set the working directory in the container
WORKDIR /app

# Copy the Gemfile and Gemfile.lock to the container
COPY Gemfile Gemfile.lock ./

# Install the Ruby dependencies
RUN apk add --update --no-cache build-base postgresql-dev nodejs tzdata \
    && gem install bundler \
    && bundle install --jobs 20 --retry 5 \
    && apk del build-base

# Copy the rest of the application code to the container
COPY . .

COPY entrypoint.sh /usr/bin/
RUN chmod +x /usr/bin/entrypoint.sh
ENTRYPOINT ["entrypoint.sh"]

# for multicontainer docker
EXPOSE 3000

CMD ["bundle", "exec", "rails", "server"]

# for single container docker
# EXPOSE 80
