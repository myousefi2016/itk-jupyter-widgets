- To release a new version of itkwidgets on PyPI:

```
export old_version=X.X.X
export version=X.X.Y

# Update itkwidgets/_version.py (set release version, remove 'dev')
git grep -z --full-name -l '.' | xargs -0 sed -i -e "s/$old_version/$version/g"
git add -- itkwidgets/ js/
git commit -m "ENH: Bump itk-jupyter-widgets to $version"
python setup.py sdist
python setup.py bdist_wheel
pip install twine
twine upload dist/*
git tag -a v$version -m "itk-jupyter-widgets $version"
# Update _version.py (add 'dev' and increment minor)
git add -- itkwidgets/_version.py
git commit -m "ENH: Bump itk-jupyter-widgets version for development"
git push
git push --tags
```

- To release a new version of itk-jupyter-widgets on NPM:

```
# clean out the `dist` and `node_modules` directories
git clean -fdx
cd js
npm install
npm publish
cd ..
```
