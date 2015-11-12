def setup
  require 'dotenv'
  Dotenv.load
  $LOAD_PATH.unshift(File.dirname(File.expand_path(__FILE__ + '/')))
end

task :test do
  require_relative './spec/spec_helper'
end

task :channels do
  setup
  api_token = ENV['KOMONJO_SLACK_API_TOKEN'] || ''
  fail 'please set ENV[KOMONJO_SLACK_API_TOKEN]' if api_token == ''
  require 'lib/services/channels_service'
  channels_service = Komonjo::Service::ChannelsService.new(api_token)
  puts channels_service.channels.map(&:name).join("\n")
end

task :messages, [:channel, :day] do |_, args|
  setup
  api_token = ENV['KOMONJO_SLACK_API_TOKEN'] || ''
  fail 'please set ENV[KOMONJO_SLACK_API_TOKEN]' if api_token == ''
  channel_name = args[:channel]
  fail 'Option -c is required!' if channel_name == ''
  require 'date'
  require 'lib/services/messages_service'

  day = Date.parse(args[:day]).to_time
  service = Komonjo::Service::MessagesService.new(api_token)
  ret = service
        .messages_with_date_filter(channel_name, day)
        .map(&:to_markdown)
        .join("\n")
  `mkdir -p md/#{channel_name}`
  File.write("./md/#{channel_name}/#{day.strftime('%Y-%m-%d')}.md", ret)
end
