---
layout: post
title: Handling File Uploads in Clojure Web Apps
author: Milinda Pathirage
time: 27th August 2012
---

[Clojure web application development](http://milinda.pathirage.org/2012/06/06/getting_started_with_clojure_web_application_development/) is still in it's early stages and there aren't lot of web applications written in Clojure. Recently I had to write add file uploading support to web application I'm developing in Clojure(using [ring](https://github.com/mmcgrana/ring) and [compojure](https://github.com/weavejester/compojure)). I found following two articles by googling, but those lacks some of the basic internal details.

* [File upload in Clojure & Compojure](http://nikola.plejic.com/blog/file-upload-in-clojure-compojure/)
* [File uploads with Clojure, Ring and Compojure](http://www.prodevtips.com/2010/12/19/file-uploads-with-clojure-ring-and-compojure/)

Rest of this post will discuss some of things I have discovered while implementing file upload support.

Below is the code for a simple compojure web application which implements file upload support.

{% highlight clojure %}
(ns file-upload.core
  (:use [compojure.core]
        [ring.middleware.params]
        [ring.middleware.multipart-params]
        [ring.adapter.jetty]
        [hiccup.core]))

(defn home-page []
  (html [:form {:action "/file" :method "post" :enctype "multipart/form-data"}
         [:input {:name "file" :type "file" :size "20"}]
         [:input {:type "submit" :name "submit" :value "submit"}]]))

(defn upload-file [file]
  (let [file-name (file :filename)
        size (file :size)]
    (do
      (copy actual-file (File. (format "/Users/milinda/Desktop/%s" file-name)))
      {:status 200
       :headers {"Content-Type" "text/html"}
       :body (html [:h1 file-name]
                   [:h1 size])})))
  
(defroutes handler
  (POST "/file" {params :params}
       (let [file (get params "file")]
         (upload-file file)))
       (home-page)))

(def app
  (-> handler
      wrap-params
      wrap-multipart-params))

{% endhighlight %}
 
To add file uploading support, you need to wrap your requests using **wrap-multipart-params** middleware which can be found in **ring.middleware.multipart-params** namespace. Previous blog posts I mentioned uses **clojure.contrib.duck-streams** module. That module is deprecated now, instead of duck-streams you can use **clojure.java.io**.

According to my HTML form file input's name is 'file'. From input parameters you can get the 'file' field and it will be a map like following.

          {:size 88855, :tempfile #<File /var/folders/hq/ym6xf4794v7g4hvhll6nmr_c0000gn/T/ring-multipart-4366831661746413539.tmp>, :content-type application/pdf, :filename slides.pdf}

From that map you can get pointer to the actual file and pther attributes like file size anf file name. Above code shows how you can save uploaded file to anywahere you like.

Complete code can be found in [github](https://github.com/milinda/ef/tree/master/clojure-web/file-upload).