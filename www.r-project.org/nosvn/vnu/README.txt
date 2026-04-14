HTML validation results for the package HTML refmans using the Nu HTML
checker (nu), see <https://validator.github.io/validator/>.

To reproduce, use something like

  install.packages("W3CMarkupValidator")
  install.packages("vnu.jar", type = "source",
                   repos = "https://datacube.wu.ac.at/")
  src <- "/path/to/PKG_VER.tar.gz"   # or just PKG if installed
  out <- "PKG.html"
  tools::pkg2HTML(src, out = out, concordance = TRUE)
  bad <- W3CMarkupValidator::w3c_markup_validate(file = out, jar = TRUE,
                                                 concordance = TRUE)
  W3CMarkupValidator::inspect(bad)  
