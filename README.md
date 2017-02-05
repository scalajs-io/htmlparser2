Htmlparser2 API for Scala.js
=======================
This is a Scala.js type-safe binding for [htmlparser2](https://www.npmjs.com/package/htmlparser2) 

A Fast & forgiving HTML/XML/RSS parser.

#### Build Dependencies

* [ScalaJs.io v0.3.x](https://github.com/ldaniels528/scalajs.io)
* [SBT v0.13.13](http://www.scala-sbt.org/download.html)

#### Build/publish the SDK locally

```bash
$ sbt clean publish-local
```

#### Running the tests

Before running the tests the first time, you must ensure the npm packages are installed:

```bash
$ npm install
```

Then you can run the tests:

```bash
$ sbt test
```

#### Examples

```scala
  val parser = new Parser(
    new ParserHandler {

      override def onopentag(name: String, attribs: js.Dictionary[String]) {
        if (name == "script" && attribs("type") == "text/javascript") {
          console.log("JS! Hooray!")
        }
      }

      override def ontext(text: String): Unit = console.log("-->", text)

      override def onclosetag(tagname: String) {
        if (tagname == "script") {
          console.log("That's it?!")
        }
      }
    },
    new ParserOptions(decodeEntities = true)
  )
  parser.write("Xyz <script type='text/javascript'>var foo = '<<bar>>'</script>")
  parser.end()
```

#### Artifacts and Resolvers

To add the `htmlparser2` binding to your project, add the following to your build.sbt:  

```sbt
libraryDependencies += "io.scalajs.npm" %%% "htmlparser2" % "0.3.0.3"
```

Optionally, you may add the Sonatype Repository resolver:

```sbt   
resolvers += Resolver.sonatypeRepo("releases") 
```