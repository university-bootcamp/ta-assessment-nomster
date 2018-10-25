# Nomster — Lesson 39 Checklist

* [Step 1 (Setting up the pipeline for photos)](https://github.com/university-bootcamp/checklist-nomster-39/compare/step-1)
* [Step 2 (Making the image field work)](https://github.com/university-bootcamp/checklist-nomster-39/compare/step-1...step-2)
* [Step 3 (Switching over to use AWS S3)](https://github.com/university-bootcamp/checklist-nomster-39/compare/step-2...step-3)

## Step 1: Setting up the pipeline for photos

* Generate a model for the photos database table.

```
rails g model photo
```

* Add the relationships in the `app/models/place.rb` and `app/models/photo.rb` files
* Update `app/controllers/places_controller.rb` in the `show` action to build a `@photo = Photo.new`
* Include the simple_form in the `app/views/places/show.html.erb`

* Generate a controller for the `photos`.

```
rails g controller photos
```

* Setup boilerplate code in the `app/controllers/photos_controller.rb`.
* Adjust the `config/routes.rb` file to connect the create action with the `place_id` in the params.
* Update the `app/views/places/show.html.erb` to make the form post to the correct URL.

## Step 2: Making the Image Field Work

* Add the gem to the `Gemfile`

```
rails g migration alter_photos_add_picture
```

* Adjust the `db/migrate/XXXXX_alter_photos_add_picture.rb` migration.
* Adjust the `app/models/photo.rb` file to mount the uploader as expected.
* *Restart the server* — skipping this step will produce a `uninitialized constant Photo::PictureUploader` error.
* Add the field in `app/views/places/show.html.erb`.
* Alter the `app/controllers/photos_controller.rb` file to include the `picture` field.
* Add the `image_tag` in the `app/views/places/show.html.erb`.

## Step 3: Setting up Image Uploading with Amazon S3

* Add `fog-aws` to `Gemfile`.
* Adjust the `config/application.yml` file (not checked into GitHub) to have this format.

```
GEOCODER_API_KEY: "xyz"
AWS_ACCESS_KEY: "xyz"
AWS_SECRET_KEY: "xyz"
AWS_BUCKET: "xyz"
```

* Create the `config/initializers/carrierwave.rb` with the relevant code.
* Switch the `app/uploaders/picture_uploader.rb` to use `:fog` instead of `:file`.