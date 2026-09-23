BASE_NAME = axioms_of_liberalism
NAME = $(BASE_NAME).xml
OUT_DIR = output
NAME_WITH_INCLUDES = $(OUT_DIR)/$(BASE_NAME).with_includes.xml
HTML_DIR = `realpath .`/$(OUT_DIR)/html/

include:
	xmllint --xinclude $(NAME) > $(NAME_WITH_INCLUDES)

validate: include
	jing ../../docbook/cdn/schema/5.2.1/rng/docbook.rng $(NAME_WITH_INCLUDES)
	# check also via old xsd, for now works even with 5.2
	xmlstarlet val --err --xsd /usr/share/xml/docbook/schema/xsd/5.0/docbook.xsd $(NAME_WITH_INCLUDES)

html: include
	rm -rf $(OUT_DIR)/html && mkdir $(OUT_DIR)/html
	java -jar ~/.local/bin/saxon-he-12.10.jar -s:$(NAME_WITH_INCLUDES) -xsl:../../docbook/cdn/release/xsltng/2.8.4/release/xslt/docbook.xsl chunk=index.html chunk-output-base-uri=file://$(HTML_DIR)

htmlpage: include # saxon 12.10 https://github.com/Saxonica/Saxon-HE/
	java -jar ~/.local/bin/saxon-he-12.10.jar -s:$(NAME_WITH_INCLUDES) -xsl:../../docbook/cdn/release/xsltng/2.8.4/release/xslt/docbook.xsl -o:$(OUT_DIR)/$(BASE_NAME).html

.SILENT:
