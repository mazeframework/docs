# Mailers

The mailer has the ability to set the`from`,`to`,`cc`,`bcc`,`subject`and`body`. You may use the`render`helper to create the body of the email.

```ruby
class WelcomeMailer < Quartz::Mailer
  def initialize
    super
    from "Maze Crystal", "info@mazecr.io"
  end

  def deliver(name: String, email: String)
    to name: name, email: email
    subject "Welcome to Maze"
    body render("mailers/welcome_mailer.slang", "mailer.slang")
    super()
  end
end
```

