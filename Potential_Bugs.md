# Potential bugs:

-----

01

If a `.md` file, such as `README.md`, contains content like:

`### FILE: something`

the importer may interpret it as a file marker and attempt to create a new file named `something`, instead of treating it as normal Markdown content.

-----
