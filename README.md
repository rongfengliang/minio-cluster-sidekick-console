# minio && console demo 


## cmd

* add s3 source

```code
mc config host add news3 http://127.0.0.1:9000 minio minio123
```

* add user

```code
mc admin user add news3/

with user console or others

```

* add policy file

```code
cat > admin.json << EOF
{
	"Version": "2012-10-17",
	"Statement": [{
			"Action": [
				"admin:*"
			],
			"Effect": "Allow",
			"Sid": ""
		},
		{
			"Action": [
                "s3:*"
			],
			"Effect": "Allow",
			"Resource": [
				"arn:aws:s3:::*"
			],
			"Sid": ""
		}
	]
}
EOF

```

* create policy

```code
mc admin policy add news3/ consoleAdmin admin.json

```

* set policy to user

```code
mc admin policy set news3 consoleAdmin user=console

```

*  login console

```code
open http://localhost:9090  user with console && console password
```