# Channels

## Introduction

All messages are routed through channels, and channel topics are where clients subscribe to listen for new messages. Channels define 3 public methods that can be used:

* `handle_joined` - Called when a user joins a channel.
* `handle_message` - Called when a user sends a message to a channel.  A common message handler will simply rebroadcast the message to the other subscribers with `rebroadcast!` method.
* `handle_leave` - Called when a user leaves the channel.

## Example Usage

A channel can be generated by calling `maze g channel ChatRoomChannel`

```ruby
class ChatRoomChannel < Maze::Websockets::Channel

  # optional
  # Authorization can happen here  
  def handle_joined(client_socket, message)
    # channel join related functionality
    # if client_socket.session[:user_id] != message["payload"]["user_id"]
    #   client_socket.disconnect!
    # end
  end

  # required
  def handle_message(client_socket, msg)
    rebroadcast!(msg)
  end

  # optional
  def handle_leave(client_socket)
    # channel leave functionality    
  end
end
```
