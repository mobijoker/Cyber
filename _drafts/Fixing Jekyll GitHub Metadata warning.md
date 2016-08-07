


https://milanaryal.com/jekyll-on-windows/

Fixing Jekyll GitHub Metadata warning

	GitHub Metadata: No GitHub API authentication could be found. Some fields may be missing or have incorrect data.


---

This is what I did to resolve this problem:

1. Create GitHub personal token ([guide](https://help.github.com/articles/creating-an-access-token-for-command-line-use/))

2. Add the JEKYLL_GITHUB_TOKEN env variable whose content is the created token

3. Download the CA cert file from https://curl.haxx.se/ca/cacert.pem
Add the SSL_CERT_FILE env variable pointing to the download .pem file.
I also wrote a blog post about this case here.

---

GitHub Metadata is a gem required by Jekyll. We need a GitHub personal token to make it work. Follow the excellent guide on GitHub to create a token, copy it to a safe place.

Now, create new environment variable in your system named JEKYLL_GITHUB_TOKEN with the value pasted from the created token. Open a new instance of command line and make sure this command displays correct information (I use Windows machine).

```
echo $JEKYLL_GITHUB_TOKEN
```

You can read more at the GitHub Metadata [README](https://github.com/jekyll/github-metadata) file.

---

I decided to play with Jekyll today. It is an amazing static site generator. I ran local server by execute this command:

```
$> jekyll serve
```

I could browse my site locally then. When I had updated one of my files, Jekyll stated regenerating the output HTML file and I got this errors on the command line window.

---

If you have recently upgraded to Jekyll v3.x.x then you may face GitHub Metadata warning (in your local development environment) if you have have use any [github-metadata](https://github.com/jekyll/github-metadata), a.k.a. `site.github` Liquid tag in your Jekyll site.

Here’s the solution to fix this warning and access GitHub Metadata on your Windows local development environment:

1. Create an GitHub access token with `public_repo` scope. (Remember to keep your tokens secret; treat them just like passwords!)

2. Now similarly as previous goto `Control Panel > System > Advances system settings` and click Environment Variables. Or simply type “environment variables” on Start menu search box.

3. Then define new user variable with variable name `JEKYLL_GITHUB_TOKEN` and GitHub access token as variable value (which is something like `abc123def456`).

4. Now click OK and Apply.

5. System reboot may needed to work for first time.

For security reason you can also access GitHub token with the following command line while building or serving Jekyll site:

```
$ JEKYLL_GITHUB_TOKEN=abc123def456 bundle exec jekyll serve
```

---

```
# Environment variables
export JEKYLL_GITHUB_TOKEN='bffcf73276b43c3ef9990319ce82b1aec9fc3c2f'
```