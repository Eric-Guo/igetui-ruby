# Igetui::Ruby

[个推](http://www.igetui.com/)服务端 ruby-sdk

## Installation

Add this line to your application's Gemfile:

    gem 'igetui-ruby', require: 'IGeTui'

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install igetui-ruby

## Usage

### Push Message To Single

    pusher = IGeTui.pusher(your_app_id, your_app_key, your_master_secret)

    # 创建通知模板
    template = IGeTui::NotificationTemplate.new
    template.logo = 'push.png'
    template.logo_url = 'http://www.igetui.com/wp-content/uploads/2013/08/logo_getui1.png'
    template.title = '测试标题'
    template.text = '测试文本'

    # 创建单体消息
    single_message = IGeTui::SingleMessage.new
    single_message.data = template

    # 创建客户端对象
    client = IGeTui::Client.new(your_client_id)

    # 发送一条通知到指定的客户端
    ret = pusher.push_message_to_single(single_message, client)
    p ret

### Push Message To List

    pusher = IGeTui.pusher(your_app_id, your_app_key, your_master_secret)

    # 创建一条透传消息
    template = IGeTui::TransmissionTemplate.new
    # Notice: content should be string.
    content = {
                action: "notification",
                title: "标题aaa",
                content: "内容",
                type: "article",
                id: "4274"
              }
    content = content.to_s.gsub(":", "").gsub("=>", ":")
    template.transmission_content = content

    # 创建群发消息
    list_message = IGeTui::ListMessage.new
    list_message.data = template

    # 创建客户端对象
    client_1 = IGeTui::Client.new(your_client_id_1)
    client_2 = IGeTui::Client.new(your_client_id_2)
    client_list = [client_1, client_2]

    content_id = pusher.get_content_id(list_message)
    ret = pusher.push_message_to_list(content_id, client_list)

### Push Message To App

    pusher = IGeTui.pusher(your_app_id, your_app_key, your_master_secret)

    # 创建通知模板
    template = IGeTui::NotificationTemplate.new
    template.logo = 'push.png'
    template.logo_url = 'http://www.igetui.com/wp-content/uploads/2013/08/logo_getui1.png'
    template.title = '测试标题'
    template.text = '测试文本'

    # 创建APP群发消息
    app_message = IGeTui::AppMessage.new
    app_message.data = template
    app_message.app_id_list = [your_app_id]

    # 发送一条通知到程序
    ret = pusher.push_message_to_app(app_message)
    p ret

### Custom Test

    require 'rubygems'
    require 'IGeTui'

    @pusher = IGeTui.pusher(your_app_id, your_app_key, your_master_secret)
    ret = @pusher.get_client_id_status(@cid_1)
    p ret

### Auto Test

    # 运行测试之前，请先修改 test/pusher_test.rb 中的相关配置
    rake test

## Contributing

1. Fork it ( http://github.com/<my-github-username>/igetui-ruby/fork )
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request
