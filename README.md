# 1) loafer_test
## Test using loafer
## docker pull pafortin/goaws
## docker run -d --name goaws -p 4100:4100 pafortin/goaws
# 2) aws --endpoint-url http://localhost:4100 sns create-topic \
  --name friend-created
# 3) aws --endpoint-url http://localhost:4100 sqs create-queue \
  --queue-name foobar-friend-created
# 4) aws --endpoint-url http://localhost:4100 sns subscribe \
  --topic-arn arn:aws:sns:local:000000000000:friend-created \
  --protocol sqs --notification-endpoint     http://localhost:4100/queue/foobar-friend-created
# 5) python -m foobar_friend_service.run
# 6) aws --endpoint-url http://localhost:4100 sns publish \
  --topic-arn arn:aws:sns:local:000000000000:friend-created \
  --message file://test_user.json