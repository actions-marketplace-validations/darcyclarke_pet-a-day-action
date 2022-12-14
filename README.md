<h3 align="center">πΆπΉπ°π±</h3>
<h3 align="center">Pet-a-Day GitHub Action</h3>

<p align="center">This action changes your GitHub/Gravatar photo to a different cute animal each day...</p>

<p align="center"><img src="https://user-images.githubusercontent.com/459713/109923925-8182d480-7c8d-11eb-80a8-430fd292d9ff.png" alt="screen2" width="80%" /></p>

## Requirements

1. Must have a [Gravatar/Wordpress.com](http://en.gravatar.com/) Account
2. Ensure the primary email you use with GitHub is associated with your Gravatar account
3. If you've previously uploaded a profile image to GitHub, "Revert to Gravatar" (re. [Settings > Profile > Edit](https://github.com/settings/profile))

<p align="center"><img src="https://user-images.githubusercontent.com/459713/109911892-fac3fc80-7c78-11eb-81fb-bbff3cc58091.png" alt="screen" width="25%" /></p>
<p align="center"><img src="https://user-images.githubusercontent.com/459713/109922257-0d473180-7c8b-11eb-991a-0aca01ce9367.png" alt="screen2" width="25%" /></p>

## Installation / Usage

1. Create a `.github/workflows/pet-a-day.yml` file in any repo...
2. Add the following...

```yaml
name: "Pet-a-Day"
on:
  schedule:
    - cron: "0 0 * * *"
jobs:
  update-avatar:
    runs-on: ubuntu-latest
    steps:
    - uses: darcyclarke/pet-a-day-action@v1.0.5
      with:
        email:  ${{ secrets.EMAIL }}
        password: ${{ secrets.PASSWORD }}
```

## Inputs

#### `email`

* **Required** The primary email used for your GitHub account
* **Note:** You should use [GitHub Action Secrets](https://docs.github.com/en/actions/reference/encrypted-secrets) to set this value (re. `https://github.com/<username>/<repo>/settings/secrets/actions`)

#### `password`

* **Required** The password associated with your Gravatar/WordPress.com account
* **Note:** You should use [GitHub Action Secrets](https://docs.github.com/en/actions/reference/encrypted-secrets) to set this value (re. `https://github.com/<username>/<repo>/settings/secrets/actions`)

#### `query`

* **Optional** Comma delimited list of categories to be used to choose the image (ex. `frogs,birds`)
* **Default** `dog,cat,dogs,cats,kittens,puppies,puppy,kitten`

## F.A.Qs

* "How long does it take to see an update?"
  * After a job run it can take a little while to see your profile update based on GitHub's caching (you can confirm a new photo was uploaded/mapped by checking [Gravatar](http://en.gravatar.com/))
* "How often does this run?"
  * Well, the cron scheduling is actually up to you... "daily" is probably nice/fine... definitely be mindful of the platform's limitations/policies though β€οΈ 
* "How does this work?"
  * Under the hood, we use [**unsplash.com**](https://unsplash.com/)'s random image endpoint along with the defined `query` (aka. "categories") param to fetch a lovely animal image, upload that to Gravatar, set it as the default profile photo & thus, setting it as your default GitHub profile photo (* if you followed the steps above of course...)
* "Why does this exist?"
  * You can thank &/or blame [**@JasonEtco**](https://github.com/JasonEtco)

<p align="center"><a href="https://twitter.com/JasonEtco/status/1367150811571175432"><img src="https://user-images.githubusercontent.com/459713/110038942-791eae00-7d0e-11eb-8685-7f39859a7040.png" alt="tweet" width="50%" /></a></p>
