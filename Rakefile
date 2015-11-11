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

task :messages, [:channel] do |_, args|
  setup
  api_token = ENV['KOMONJO_SLACK_API_TOKEN'] || ''
  fail 'please set ENV[KOMONJO_SLACK_API_TOKEN]' if api_token == ''
  channel_name = args[:channel]
  fail 'Option -c is required!' if channel_name == ''

  require 'lib/services/messages_service'
  messages_service = Komonjo::Service::MessagesService.new(api_token)
  ret = messages_service.messages(channel_name).map(&:to_markdown).join("\n")
  filename = args[:filename] || ''
  if filename == ''
    puts ret
  else
    File.write("./md/#{filename}", ret)
  end
end
