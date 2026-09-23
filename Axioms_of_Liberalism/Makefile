BASE_NAME = axioms_of_liberalism
NAME = $(BASE_NAME).xml
NAME_WITH_INCLUDES = $(BASE_NAME).with_includes.xml


include:
	xmllint --xinclude $(NAME) > $(NAME_WITH_INCLUDES)

validate: include
	jing ../../docbook/cdn/schema/5.2.1/rng/docbook.rng $(NAME_WITH_INCLUDES)
	xmlstarlet val --err --xsd /usr/share/xml/docbook/schema/xsd/5.0/docbook.xsd $(NAME_WITH_INCLUDES)

htmlpage: include # saxon 12.10 https://github.com/Saxonica/Saxon-HE/
	java -jar ~/.local/bin/saxon-he-12.10.jar -s:$(NAME_WITH_INCLUDES) -xsl:../../docbook/cdn/release/xsltng/2.8.4/release/xslt/docbook.xsl -o:$(BASE_NAME).html

.SILENT:
