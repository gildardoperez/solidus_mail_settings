# Solidus Mail Settings

[![Build Status](https://travis-ci.org/spree-contrib/spree_mail_settings.svg?branch=master)](https://travis-ci.org/spree-contrib/spree_mail_settings)
[![Code Climate](https://codeclimate.com/github/spree-contrib/spree_mail_settings/badges/gpa.svg)](https://codeclimate.com/github/spree-contrib/spree_mail_settings)

---

## Installation

1. Add this extension to your Gemfile with this line:
  ```ruby
  gem 'solidus_mail_settings', github: '2bedigital/solidus_mail_settings', branch: 'master'
  ```

2. Install the gem using Bundler:
  ```ruby
  bundle install
  ```

3. Restart your server

  If your server was running, restart it so that it can find the assets properly.

3. Update the Settings:
  https://www.xyzcompany.xyz/admin/mail_method/edit
  
4. Issue in production were settings in the backend reset:
  Create file:
    touch app/models/spree/app_configuration_decorator.rb
      add:
      ```
      module Spree
      AppConfiguration.class_eval do
        # Default mail headers settings
        preference :mails_from, :string, default: 'orders@xyzcompany.xyz'
        preference :enable_mail_delivery, :boolean, default: false
        preference :mail_bcc, :string, default: 'hello@xyzcompany.xyz'
        preference :intercept_email, :string, default: nil

        # Default smtp settings
        preference :mail_host, :string, default: 'us-west-2.amazonses.com'
        preference :mail_domain, :string, default: 'email-smtp.us-west-2.amazonaws.com'
        preference :mail_port, :integer, default: 465
        preference :secure_connection_type, :string, default: Core::MailSettings::SECURE_CONNECTION_TYPES[2]
        preference :mail_auth_type, :string, default: Core::MailSettings::MAIL_AUTH[2]
        preference :smtp_username, :string, default: ENV['SMTP_USERNAME']
        preference :smtp_password, :string, default: ENV['SMTP_PASSWORD']

        def override_actionmailer_config
          raise 'override_actionmailer_config has been removed. ' \
                'actionmailer\'s config is always overwridden when spree_mail_settings is included'
        end
        alias_method :override_actionmailer_config=, :override_actionmailer_config
      end
    end

      ```

  

---

## Contributing

See corresponding [guidelines][4]

---

## License

Copyright (c) 2014-2015 [John Hawthorn][1] and [contributors][2], released under the [New BSD License][3]

[1]: https://github.com/jhawthorn
[2]: https://github.com/spree-contrib/spree_mail_settings/graphs/contributors
[3]: https://github.com/spree-contrib/spree_mail_settings/tree/master/LICENSE.md
[4]: https://github.com/spree-contrib/spree_mail_settings/tree/master/CONTRIBUTING.md
