# Fluent::Plugin::Kafka

TODO: Write a gem description
TODO: Also, I need to write tests

## Installation

Add this line to your application's Gemfile:

    gem 'fluent-plugin-kafka'

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install fluent-plugin-kafka

## Usage

### Input plugin

    <source>
      type   kafka
      host   <broker host>
      port   <broker port: default=9092>
      topics <listening topics(separate with comma',')>
      format <input text type (text|json|ltsv|msgpack)>
      add_prefix <tag prefix (Optional)>
      add_suffix <tag suffix (Optional)>
    </source>

### Output plugin (non-buffered)

    <match *.**>
      type                kafka
      brokers             <broker1_host>:<broker1_ip>,<broker2_host>:<broker2_ip>,..
      default_topic       <output topic>
      output_data_type    (json|ltsv|msgpack|attr:<record name>)
      output_include_tag  (true|false) :default => false
      output_include_time (true|false) :default => false
      max_send_retries    (integer)    :default => 3
      required_acks       (integer)    :default => 0
      ack_timeout_ms      (integer)    :default => 1500
    </match>

Supports following Poseidon::Producer options.

- max_send_retries — default: 3 — Number of times to retry sending of messages to a leader.
- required_acks — default: 0 — The number of acks required per request.
- ack_timeout_ms — default: 1500 — How long the producer waits for acks.

See also [Poseidon::Producer](http://www.rubydoc.info/github/bpot/poseidon/Poseidon/Producer) for more detailed documentation about Poseidon.

### Buffered output plugin

    <match *.**>
      type                kafka_buffered
      brokers             <broker1_host>:<broker1_ip>,<broker2_host>:<broker2_ip>,..
      default_topic       <output topic>
      flush_interval      <flush interval (sec) :default => 60>
      buffer_type         (file|memory)
      output_data_type    (json|ltsv|msgpack|attr:<record name>)
      output_include_tag  (true|false) :default => false
      output_include_time (true|false) :default => false
      max_send_retries    (integer)    :default => 3
      required_acks       (integer)    :default => 0
      ack_timeout_ms      (integer)    :default => 1500
    </match>

Supports following Poseidon::Producer options.

- max_send_retries — default: 3 — Number of times to retry sending of messages to a leader.
- required_acks — default: 0 — The number of acks required per request.
- ack_timeout_ms — default: 1500 — How long the producer waits for acks.

See also [Poseidon::Producer](http://www.rubydoc.info/github/bpot/poseidon/Poseidon/Producer) for more detailed documentation about Poseidon.


## Contributing

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Added some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request
