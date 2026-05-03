# Observer

Notify all when one changes.

## Example
Youtube Channel -> Subscribers get notifications



```java
interface Subscriber{
    void notify(String video);
}

class YoutubeChannel{
    private List<Subscriber> subs = new ArrayList<>();

    // Attach/add an abserver to the list
    void register(Subscriber s){
        subs.add(s);
    }

    void deregister(Subscriber s){
        subs.remove(s);
    }

    void uploadVideo(String tittle){
        SOP("Video uploaded");
        notifyObervers("VideoTittle");
    }

    void notifyObservers(String tittle){
        for(Subscriber s : subs){
            s.notify("New video Uploaded");
        }
    }
}

class User implements Subscriber{
    public void notify(string message){

    }
}

YoutubeChannel channel = new YoutubeChannel();
User user = new User();
channel.register(user);
channel.notifyObservers();
channel.uploadVideo("Video");


```