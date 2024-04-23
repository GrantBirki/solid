# Dependency Inversion

> *Depend upon abstractions, not concretes.*

Dependency Inversion Principle (DIP) is a specific aspect of Inversion of Control (IoC) that states that high-level modules should not depend on low-level modules, but both should depend on abstractions.

In Ruby, this often translates to using interfaces or abstract classes to define dependencies, allowing for interchangeable implementations.

## Basic Example

```ruby
# Define an abstract class or interface
class NotificationSender
  def send_notification(to, message)
    # raise an error if the subclasses did not implement the required send_notification method
    raise NotImplementedError, "Subclasses must implement send_notification method"
  end
end

# Implement a concrete class that depends on the abstract class
class EmailSender < NotificationSender
  def send_notification(to, message)
    # Code to send email
    puts "Email sent to #{to}: #{message}"
  end
end

class SMSSender < NotificationSender
  def send_notification(to, message)
    # Code to send SMS
    puts "SMS sent to #{to}: #{message}"
  end
end

# High-level module that depends on the abstract class/interface
class NotificationService
  def initialize(sender)
    @sender = sender
  end

  def send_notification(to, message)
    @sender.send_notification(to, message)
  end
end

# Usage
email_sender = EmailSender.new
notification_service = NotificationService.new(email_sender)
notification_service.send_notification("example@example.com", "Hello from Dependency Inversion!")

sms_sender = SMSSender.new
notification_service = NotificationService.new(sms_sender)
notification_service.send_notification("555-1234", "Hello from Dependency Inversion!")
```
