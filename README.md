<p align="center">
  <a href="https://www.notif.me">
    <img alt="Notif.me" src="https://notifme.github.io/notifme-sdk/img/logo.png" />
  </a>
</p>

<p align="center">
  Blog of Notif.me, a solution to send all kinds of transactional notifications.
</p>

## Run in local

```shell
$ docker run --name notifme-sdk-blog --volume=$PWD:/srv/jekyll -p 35729:35729 -p 4000:4000 -it jekyll/jekyll jekyll serve
```

Then go to [localhost:4000](http://localhost:4000/).

## Contributing

To get started: [fork](https://help.github.com/articles/fork-a-repo/) this repository to your own GitHub account and then [clone](https://help.github.com/articles/cloning-a-repository/) it to your local device.

```shell
$ git clone git@github.com:[YOUR_USERNAME]/notifme-sdk-blog.git && cd notifme-sdk-blog
```
