# Build inside the correct Docker image
# AWS publishes Glue container images on ECR Public. Use them to guarantee compatibility.

```bash
docker run --rm \
  -v $(pwd)/dist:/output \
  amazon/aws-glue-libs:glue_libs_4.0.0_image_01 \
  /bin/bash -c "
    pip install \
      --platform manylinux2014_x86_64 \
      --implementation cp \
      --python-version 3.10 \
      --only-binary=:all: \
      --target /output \
      psycopg2-binary
  "
```

This produces the correct manylinux wheel inside ./dist/.
. Zip the package (Glue requires a .zip for --additional-python-modules or egg/wheel path)

```bash
cd dist
zip -r ../psycopg2_binary_glue4.zip .
cd ..`
```
