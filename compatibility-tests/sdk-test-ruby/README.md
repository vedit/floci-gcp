# Ruby SDK compatibility

Ruby 3.4 with locked official Google Cloud clients and Minitest. This initial
suite covers GCS byte transfers, metadata, pagination, range reads, resumable
uploads, signed transfer URL shape and supported downscoped prefix grants.
Credentials and fixture data are synthetic.

Build with `docker build -t floci-sdk-ruby .`. Run on the same Docker network as
the emulator, set `FLOCI_GCP_ENDPOINT` to its HTTP origin, and mount a writable
directory at `/results` for JUnit output. The entrypoint runs `test/all.rb`.

The compatibility workflow runs this suite; the cache-warming workflow watches
Gemfile and Gemfile.lock and uses the matching runner architecture and cache
scope. PR jobs remain read-only cache consumers.

Signed transfers verify URL shape and bytes, not cryptographic signature
enforcement. Downscoped checks cover the supported CAB subset, not full IAM.
Additional Compute, Monitoring, multipart and restart contracts are proposed
separately after their emulator prerequisites land.
