---
title: AdminClient Configuration
category: Apache Kafka
order: 9
permalink: /Apache%20Kafka/adminclient-configuration/
description: 아파치 카프카 공식 문서에 있는 어드민 클라이언트 설정을 한국어로 번역한 문서입니다.
image: ./../../images/kafka/logo.png
lastmod: 2021-02-14T22:25:00+09:00
comments: true
originalRefName: 아파치 카프카
originalRefLink: https://kafka.apache.org/27/documentation.html#adminclientconfigs
---

---

## 3.7 Admin Configs

다음은 카프카 어드민 클라이언트 라이브러리의 설정이다.

- #### bootstrap.servers

  카프카 클러스터에 대한 초기 커넥션을 구축하는 데 사용할 호스트/포트 쌍 리스트. 클라이언트가 부트스트랩될 땐 여기에 지정한 서버랑은 상관 없이 모든 서버를 사용하게 된다 — 이 리스트에 따라 전체 서버 셋을 발견하기 위한 초기 호스트만 달리질 뿐이다. 리스트엔 `host1:port1,host2:port2,...` 포맷을 사용해야 한다. 이 서버들은 전체 클러스터 멤버십(동적으로 변경될 수 있음)을 발견하기 위한 초기 커넥션에만 사용하기 때문에, 모든 서버를 다 넣어야 하는 건 아니다 (단, 서버 하나가 다운됐다면 최소 두 개가 필요할 순 있다).

  |         Type: | list |
  | ------------: | ---- |
  |      Default: |      |
  | Valid Values: |      |
  |   Importance: | high |

- #### ssl.key.password

  keystore 파일의 개인키 또는 [`ssl.keystore.key`](#sslkeystorekey)에 지정한 PEM 키의 패스워드. 클라이언트에선 양방향 인증을 설정했을 때만 필요하다.

  |         Type: | password |
  | ------------: | -------- |
  |      Default: | null     |
  | Valid Values: |          |
  |   Importance: | high     |

- #### ssl.keystore.certificate.chain

  '[ssl.keystore.type](#sslkeystoretype)'에 지정한 포맷을 사용한 인증서 체인. 디폴트 SSL 엔진 팩토리는 X.509 인증서 리스트를 가진 PEM 형식만 지원한다.

  |         Type: | password |
  | ------------: | -------- |
  |      Default: | null     |
  | Valid Values: |          |
  |   Importance: | high     |

- #### ssl.keystore.key

  '[ssl.keystore.type](#sslkeystoretype)'에 지정한 포맷을 사용한 개인키. 디폴트 SSL 엔진 팩토리는 PKCS#8 키를 가진 PEM 형식만 지원한다. 키가 암호화됐다면 '[ssl.key.password](#sslkeypassword)'를 통해 키 비밀번호를 지정해야 한다.

  |         Type: | password |
  | ------------: | -------- |
  |      Default: | null     |
  | Valid Values: |          |
  |   Importance: | high     |

- #### ssl.keystore.location

  keystore 파일의 위치. 클라이언트에선 선택 사항이다. 클라이언트에선 양방향 인증에 사용할 수 있다.

  |         Type: | string |
  | ------------: | ------ |
  |      Default: | null   |
  | Valid Values: |        |
  |   Importance: | high   |

- #### ssl.keystore.password

  keystore 파일의 저장소 패스워드. 클라이언트에선 선택 사항이며, '[ssl.keystore.location](#sslkeystorelocation)'을 설정했을 때만 필요하다. PEM 형식에는 keystore 패스워드를 지원하지 않는다.

  |         Type: | password |
  | ------------: | -------- |
  |      Default: | null     |
  | Valid Values: |          |
  |   Importance: | high     |

- #### ssl.truststore.certificates

  '[ssl.truststore.type](#ssltruststoretype)'에 지정한 포맷을 사용한 신뢰할 수 있는 인증서. 디폴트 SSL 엔진 팩토리는 X.509 인증서를 가진 PEM 형식만 지원한다.

  |         Type: | password |
  | ------------: | -------- |
  |      Default: | null     |
  | Valid Values: |          |
  |   Importance: | high     |

- #### ssl.truststore.location

  truststore 파일의 위치.

  |         Type: | string |
  | ------------: | ------ |
  |      Default: | null   |
  | Valid Values: |        |
  |   Importance: | high   |

- #### ssl.truststore.password

  truststore 파일의 패스워드. 패스워드를 설정하지 않으면 설정한 truststore 파일을 사용할 순 있지만 무결성 검사는 비활성화된다. PEM 형식에는 truststore 패스워드를 지원하지 않는다.

  |         Type: | password |
  | ------------: | -------- |
  |      Default: | null     |
  | Valid Values: |          |
  |   Importance: | high     |

- #### client.dns.lookup

  클라이언트가 DNS lookup을 사용하는 방법을 제어한다. `use_all_dns_ips`로 설정하면, 연결에 성공할 때까지 반환된 각 IP 주소에 순서대로 연결한다. 연결이 끊어지면 다음 IP를 사용한다. 모든 IP를 한 번씩 사용하고나면 클라이언트는 호스트명으로 IP(s)를 다시 리졸브한다 (단, JVM, OS 모두 DNS name lookup을 캐시해둔다). `resolve_canonical_bootstrap_servers_only`로 설정하면, 각 부트스트랩 주소를 canonical name 리스트로 리졸브한다. 부트스트랩 단계 이후에는 `use_all_dns_ips`와 동일하게 동작한다. `default` (deprecated)로 설하면, lookup에서 IP 주소를 여러 개 반환하더라도, 첫 번째로 반환된 IP 주소에 연결을 시도한다.

  |         Type: | string                                                       |
  | ------------: | ------------------------------------------------------------ |
  |      Default: | use_all_dns_ips                                              |
  | Valid Values: | [default, use_all_dns_ips, resolve_canonical_bootstrap_servers_only] |
  |   Importance: | medium                                                       |

- #### client.id

  요청을 보낼 때 서버에 전달할 문자열 id. id를 사용하는 목적은 서버 측 요청 로그에 논리적인 어플리케이션명을 추가해서, IP/포트를 외로도 요청 주체를 추적할 수 있도록 하기 위함이다.

  |         Type: | string |
  | ------------: | ------ |
  |      Default: | ""     |
  | Valid Values: |        |
  |   Importance: | medium |

- #### connections.max.idle.ms

  유휴 커넥션은 이 설정에 지정한 시간(밀리세컨드)이 지나면 종료한다.

  |         Type: | long               |
  | ------------: | ------------------ |
  |      Default: | 300000 (5 minutes) |
  | Valid Values: |                    |
  |   Importance: | medium             |

- #### default.api.timeout.ms

  클라이언트 API의 타임아웃(밀리세컨드 단위)을 지정한다. 이 설정은 timeout 파라미터를 지정하지 않은 모든 클라이언트 연산에 대한 기본 타임아웃으로 사용한다.

  |         Type: | int              |
  | ------------: | ---------------- |
  |      Default: | 60000 (1 minute) |
  | Valid Values: | [0,...]          |
  |   Importance: | medium           |

- #### receive.buffer.bytes

  데이터를 읽을 때 사용하는 TCP 수신 버퍼(SO_RCVBUF)의 크기. 값이 -1이면 OS 기본값을 사용한다.

  |         Type: | int                  |
  | ------------: | -------------------- |
  |      Default: | 65536 (64 kibibytes) |
  | Valid Values: | [-1,...]             |
  |   Importance: | medium               |

- #### request.timeout.ms

  이 설정은 클라이언트가 응답을 기다릴 최대 시간을 제어한다. 클라이언트는 타임 아웃될 때까지 응답을 받지 못하면, 필요한 경우 요청을 재전송할 수 있으며, 재시도 횟수를 모두 소진하면 요청은 실패로 끝난다.

  |         Type: | int                |
  | ------------: | ------------------ |
  |      Default: | 30000 (30 seconds) |
  | Valid Values: | [0,...]            |
  |   Importance: | medium             |

- #### sasl.client.callback.handler.class

  AuthenticateCallbackHandler 인터페이스를 구현한 SASL 클라이언트 콜백 핸들러 클래스의 풀 네임(fully qualified name).

  |         Type: | class  |
  | ------------: | ------ |
  |      Default: | null   |
  | Valid Values: |        |
  |   Importance: | medium |

- #### sasl.jaas.config

  JAAS 설정 파일 포맷에 있는, SASL 연결을 위한 JAAS 로그인 컨텍스트 파라미터. JAAS 설정 파일 포맷은 여기에서 설명하고 있다. 이 값에 사용하는 포맷은 ‘loginModuleClass controlFlag (optionName=optionValue)*;‘이다. 브로커에선 앞에 listener와 소문자로된 SASL 메커니즘 이름을 지정해야 한다. 예를 들어, listener.name.sasl_ssl.scram-sha-256.sasl.jaas.config=com.example.ScramLoginModule required;

  |         Type: | password |
  | ------------: | -------- |
  |      Default: | null     |
  | Valid Values: |          |
  |   Importance: | medium   |

- #### sasl.kerberos.service.name

  카프카가 실행되는 커버로스 principal 이름. 카프카의 JAAS 설정으로도 정의할 수 있고, 카프카 설정에서도 정의할 수 있다.

  |         Type: | string |
  | ------------: | ------ |
  |      Default: | null   |
  | Valid Values: |        |
  |   Importance: | medium |

- #### sasl.login.callback.handler.class

  AuthenticateCallbackHandler 인터페이스를 구현한 SASL 로그인 콜백 핸들러 클래스의 풀 네임(fully qualified name). 브로커에선 앞에 listener와 소문자로된 SASL 메커니즘 이름을 지정해야 한다. 예를 들면, listener.name.sasl_ssl.scram-sha-256.sasl.login.callback.handler.class=com.example.CustomScramLoginCallbackHandler

  |         Type: | class  |
  | ------------: | ------ |
  |      Default: | null   |
  | Valid Values: |        |
  |   Importance: | medium |

- #### sasl.login.class

  Login 인터페이스를 구현한 클래스의 풀 네임(fully qualified name). 브로커에선 앞에 listener와 소문자로된 SASL 메커니즘 이름을 지정해야 한다. 예를 들어, listener.name.sasl_ssl.scram-sha-256.sasl.login.class=com.example.CustomScramLogin

  |         Type: | class  |
  | ------------: | ------ |
  |      Default: | null   |
  | Valid Values: |        |
  |   Importance: | medium |

- #### sasl.mechanism

  클라이언트 커넥션에 사용할 SASL 메커니즘. 시큐리티 프로바이더를 사용할 수 있는 메커니즘이라면 다 가능하다. GSSAPI가 디폴트 메커니즘이다.

  |         Type: | string |
  | ------------: | ------ |
  |      Default: | GSSAPI |
  | Valid Values: |        |
  |   Importance: | medium |

- #### security.protocol

  브로커와 통신할 때 사용하는 프로토콜. 유효한 값은 PLAINTEXT, SSL, SASL_PLAINTEXT, SASL_SSL이다.

  |         Type: | string    |
  | ------------: | --------- |
  |      Default: | PLAINTEXT |
  | Valid Values: |           |
  |   Importance: | medium    |

- #### send.buffer.bytes

  데이터를 전송할 때 사용하는 TCP 전송 버퍼(SO_SNDBUF)의 크기. 값이 -1이면 OS 기본값을 사용한다.

  |         Type: | int                    |
  | ------------: | ---------------------- |
  |      Default: | 131072 (128 kibibytes) |
  | Valid Values: | [-1,...]               |
  |   Importance: | medium                 |

- #### socket.connection.setup.timeout.max.ms

  클라이언트가 소켓 커넥션이 구축될 때까지 기다릴 최대 시간. 연이어서 커넥션 연결에 실패하면 매번 실패할 때마다 커넥션 세팅 타임아웃이 늘어나, 순식간에 이 최대값까지 커질 수 있다. 커넥션 폭풍을 방지하기 위해 타임아웃에 랜덤화 계수 0.2를 적용해, 계산된 값보다 20% 아래 ~ 20% 위까지의 랜덤 범위를 만든다.

  |         Type: | long                 |
  | ------------: | -------------------- |
  |      Default: | 127000 (127 seconds) |
  | Valid Values: |                      |
  |   Importance: | medium               |

- #### socket.connection.setup.timeout.ms

  클라이언트가 소켓 커넥션이 구축될 때까지 기다리는 시간. 타임아웃되기 전에 커넥션이 구축되지 않으면 클라이언트는 소켓 채널을 닫는다.

  |         Type: | long               |
  | ------------: | ------------------ |
  |      Default: | 10000 (10 seconds) |
  | Valid Values: |                    |
  |   Importance: | medium             |

- #### ssl.enabled.protocols

  SSL 커넥션에 활성화할 프로토콜 리스트. 자바 11 이상에서 실행하면 기본값은 'TLSv1.2,TLSv1.3'이며, 그 외는 'TLSv1.2'다. 자바 11 기본값에선 클라이언트와 서버 둘 다 지원한다면 TLSv1.3을, 그외는 TLSv1.2로 폴백한다 (둘 다 최소 TLSv1.2는 지원한다고 가정). 대부분은 이 기본값으로도 충분하다. [`ssl.protocol`](#sslprotocol) 설정도 참고해라.

  |         Type: | list    |
  | ------------: | ------- |
  |      Default: | TLSv1.2 |
  | Valid Values: |         |
  |   Importance: | medium  |

- #### ssl.keystore.type

  keystore 파일의 파일 포맷. 클라이언트에선 선택 사항이다.

  |         Type: | string |
  | ------------: | ------ |
  |      Default: | JKS    |
  | Valid Values: |        |
  |   Importance: | medium |

- #### ssl.protocol

  SSLContext를 생성할 때 사용할 SSL 프로토콜. 자바 11 이상에서 실행하면 기본값은 'TLSv1.3'이며, 그 외는 'TLSv1.2'다. 대부분은 이 기본값으로도 충분하다. 최신 JVM에서 허용하는 값은 'TLSv1.2'과 'TLSv1.3'이다. 구버전 JVM에선 'TLS', 'TLSv1.1', 'SSL', 'SSLv2', 'SSLv3'을 지원할 수도 있지만, 보안 취약점이 알려져 있어서 사용하지 않는 게 좋다. 이 설정과 '[ssl.enabled.protocols](#sslenabledprotocols)'에 기본값을 사용하면, 서버가 'TLSv1.3'을 지원하지 않는 경우엔 클라이언트는 'TLSv1.2'로 다운그레이드된다. 이 설정을 'TLSv1.2'로 지정하면, [ssl.enabled.protocols](#sslenabledprotocols)에 'TLSv1.3'이 있고 서버는 'TLSv1.3'만 지원하더라도, 클라이언트는 'TLSv1.3'을 사용하지 않는다.

  |         Type: | string  |
  | ------------: | ------- |
  |      Default: | TLSv1.2 |
  | Valid Values: |         |
  |   Importance: | medium  |

- #### ssl.provider

  SSL 커넥션에 사용할 시큐리티 프로바이더 이름. 기본값은 JVM의 디폴트 시큐리티 프로바이더다.

  |         Type: | string |
  | ------------: | ------ |
  |      Default: | null   |
  | Valid Values: |        |
  |   Importance: | medium |

- #### ssl.truststore.type

  truststore 파일의 파일 포맷.

  |         Type: | string |
  | ------------: | ------ |
  |      Default: | JKS    |
  | Valid Values: |        |
  |   Importance: | medium |

- #### metadata.max.age.ms

  새로운 브로커나 파티션을 사전에 발견할 수 있도록, 파티션 리더십이 변경되지 않아도 메타데이터를 강제로 리프레시할 간격 (밀리세컨드).

  |         Type: | long               |
  | ------------: | ------------------ |
  |      Default: | 300000 (5 minutes) |
  | Valid Values: | [0,...]            |
  |   Importance: | low                |

- #### metric.reporters

  메트릭 리포터로 사용할 클래스 리스트. `org.apache.kafka.common.metrics.MetricsReporter` 인터페이스를 구현하면 새 메트릭을 생성을 통지 받을 클래스를 연결할 수 있다. JMX 통계를 등록하는 JmxReporter는 항상 추가된다.

  |         Type: | list |
  | ------------: | ---- |
  |      Default: | ""   |
  | Valid Values: |      |
  |   Importance: | low  |

- #### metrics.num.samples

  메트릭 계산을 위해 유지할 샘플 수.

  |         Type: | int     |
  | ------------: | ------- |
  |      Default: | 2       |
  | Valid Values: | [1,...] |
  |   Importance: | low     |

- #### metrics.recording.level

  메트릭을 기록할 제일 높은 레벨.

  |         Type: | string               |
  | ------------: | -------------------- |
  |      Default: | INFO                 |
  | Valid Values: | [INFO, DEBUG, TRACE] |
  |   Importance: | low                  |

- #### metrics.sample.window.ms

  메트릭 샘플을 계산할 시간 윈도우.

  |         Type: | long               |
  | ------------: | ------------------ |
  |      Default: | 30000 (30 seconds) |
  | Valid Values: | [0,...]            |
  |   Importance: | low                |

- #### reconnect.backoff.max.ms

  브로커에 연결을 반복해서 실패했을 때, 다시 연결해보기까지 대기하는 최대 시간 (밀리세컨드). 연이어서 커넥션 연결에 실패하면 매번 실패할 때마다 호스트 당 백오프 값이 늘어나, 순식간에 이 최대값까지 커질 수 있다. 커넥션 폭풍을 방지하기 위해 백오프 증가값을 계산한 후에 20% 랜덤 지터를 추가한다.

  |         Type: | long            |
  | ------------: | --------------- |
  |      Default: | 1000 (1 second) |
  | Valid Values: | [0,...]         |
  |   Importance: | low             |

- #### reconnect.backoff.ms

  주어진 호스트에 연결을 다시 시도하기 전 대기하는 기본 시간. 리소스를 차지한채 반복문으로 계속해서 같은 호스트에 연결하는 것을 방지한다. 이 백오프는 클라이언트가 브로커에 연결을 시도하는 모든 곳에 적용된다.

  |         Type: | long    |
  | ------------: | ------- |
  |      Default: | 50      |
  | Valid Values: | [0,...] |
  |   Importance: | low     |

- #### retries

  0보다 크게 설정하면, 클라이언트는 일시적인 오류로 실패한 모든 요청를 다시 전송한다. 이 값은 0이나 `MAX_VALUE`로 설정하고, 그에 맞는 타임 아웃 파라미터로 클라이언트가 요청을 재시도하는 전체적인 시간을 제어하는 것을 권장한다.

  |         Type: | int                |
  | ------------: | ------------------ |
  |      Default: | 2147483647         |
  | Valid Values: | [0,...,2147483647] |
  |   Importance: | low                |

- #### retry.backoff.ms

  실패한 요청을 재시도하기 전 대기하는 시간. 일부 실패 시나리오에서 리소스를 차지한채 반복문으로 계속해서 요청을 보내는 것을 방지한다.

  |         Type: | long    |
  | ------------: | ------- |
  |      Default: | 100     |
  | Valid Values: | [0,...] |
  |   Importance: | low     |

- #### sasl.kerberos.kinit.cmd

  커버로스 kinit 커맨드 경로.

  |         Type: | string         |
  | ------------: | -------------- |
  |      Default: | /usr/bin/kinit |
  | Valid Values: |                |
  |   Importance: | low            |

- #### sasl.kerberos.min.time.before.relogin

  리프레시 시도 간격 (로그인 스레드 sleep 시간).

  |         Type: | long  |
  | ------------: | ----- |
  |      Default: | 60000 |
  | Valid Values: |       |
  |   Importance: | low   |

- #### sasl.kerberos.ticket.renew.jitter

  갱신 시간에 추가되는 랜덤 지터 백분율.

  |         Type: | double |
  | ------------: | ------ |
  |      Default: | 0.05   |
  | Valid Values: |        |
  |   Importance: | low    |

- #### sasl.kerberos.ticket.renew.window.factor

  로그인 스레드는 마지막 갱신 시각부터 티켓 만료 시간까지 남은 시간이, 지정한 지정한 윈도우 팩터만큼 지날 때까지 일시정지하며(sleep), 윈도우 팩터에 도달하면 티켓 갱신을 시도한다.

  |         Type: | double |
  | ------------: | ------ |
  |      Default: | 0.8    |
  | Valid Values: |        |
  |   Importance: | low    |

- #### sasl.login.refresh.buffer.seconds

  credential을 리프레시할 때, credential을 만료하기 전 유지할 버퍼 시간 (초 단위). 리프레시하려던 시간이 버퍼 시간보다 늦다면, 리프레시 시간을 앞당겨 가능한 한 버퍼 시간을 유지한다. 유효한 값은 0에서 3600(1시간) 사이다. 값을 지정하지 않으면 기본값 300(5분)을 사용한다. 이 값과 [sasl.login.refresh.min.period.seconds](#saslloginrefreshminperiodseconds)의 합이 credential의 남은 수명을 넘어가면 둘다 무시된다. 현재는 OAUTHBEARER에만 적용된다.

  |         Type: | short        |
  | ------------: | ------------ |
  |      Default: | 300          |
  | Valid Values: | [0,...,3600] |
  |   Importance: | low          |

- #### sasl.login.refresh.min.period.seconds

  credential을 리프레시하기 전에 로그인 리프레시 스레드가 대기할 최소 시간 (초 단위). 유효한 값은 0에서 900(15분) 사이다. 값을 지정하지 않으면 기본값 60(1분)을 사용한다. 이 값과 [sasl.login.refresh.buffer.seconds](#saslloginrefreshbufferseconds)의 합이 credential의 남은 수명을 넘어가면 둘다 무시된다. 현재는 OAUTHBEARER에만 적용된다.

  |         Type: | short       |
  | ------------: | ----------- |
  |      Default: | 60          |
  | Valid Values: | [0,...,900] |
  |   Importance: | low         |

- #### sasl.login.refresh.window.factor

  로그인 리프레시 스레드는 credential의 수명이 지정한 윈도우 팩터만큼 지날 때까지 일시정지하며(sleep), 윈도우 팩터에 도달하면 credential 리프레시를 시도한다. 유효한 값은 0.5(50%)에서 1.0(100%) 사이다. 값을 지정하지 않으면 기본값 0.8(80%)을 사용한다. 현재는 OAUTHBEARER에만 적용된다.

  |         Type: | double        |
  | ------------: | ------------- |
  |      Default: | 0.8           |
  | Valid Values: | [0.5,...,1.0] |
  |   Importance: | low           |

- #### sasl.login.refresh.window.jitter

  로그인 리프레시 스레드의 sleep 시간에 추가되는, credential의 수명 계산에 사용할 랜덤 지터의 최대 크기. 유효한 값은 0부터 0.25(25%) 이하다. 값을 지정하지 않으면 기본값 0.05(5%)를 사용한다. 현재는 OAUTHBEARER에만 적용된다.

  |         Type: | double         |
  | ------------: | -------------- |
  |      Default: | 0.05           |
  | Valid Values: | [0.0,...,0.25] |
  |   Importance: | low            |

- #### security.providers

  보안 알고리즘을 구현한 프로바이더를 반환하는 설정 가능한 Creator 클래스 리스트. 이 클래스는 `org.apache.kafka.common.security.auth.SecurityProviderCreator` 인터페이스를 구현해야 한다.

  |         Type: | string |
  | ------------: | ------ |
  |      Default: | null   |
  | Valid Values: |        |
  |   Importance: | low    |

- #### ssl.cipher.suites

  암호화 스위트 리스트. 암호와 스위트는 TLS나 SSL 네트워크 프로토콜로 네트워크 커넥션 보안 설정을 협상하는 데 사용되는 인증, 암호화, MAC, 키 교환 알고리즘을 하나로 조합해놓은 집합이다. 기본적으로는 가능한 모든 암호화 스위트를 지원한다.

  |         Type: | list |
  | ------------: | ---- |
  |      Default: | null |
  | Valid Values: |      |
  |   Importance: | low  |

- #### ssl.endpoint.identification.algorithm

  서버 인증서를 사용해 서버 호스트명을 검증하는 엔드포인트 식별 알고리즘.

  |         Type: | string |
  | ------------: | ------ |
  |      Default: | https  |
  | Valid Values: |        |
  |   Importance: | low    |

- #### ssl.engine.factory.class

  SSLEngine 객체를 제공하는 org.apache.kafka.common.security.auth.SslEngineFactory 타입 클래스. 기본값은 org.apache.kafka.common.security.ssl.DefaultSslEngineFactory다.

  |         Type: | class |
  | ------------: | ----- |
  |      Default: | null  |
  | Valid Values: |       |
  |   Importance: | low   |

- #### ssl.keymanager.algorithm

  SSL 커넥션에서 키 매니저 팩토리가 사용할 알고리즘. 기본값은 자바 가상 머신에 설정된 키 매니저 팩토리 알고리즘이다.

  |         Type: | string  |
  | ------------: | ------- |
  |      Default: | SunX509 |
  | Valid Values: |         |
  |   Importance: | low     |

- #### ssl.secure.random.implementation

  SSL 암호화 연산에 사용할 SecureRandom PRNG 구현체.

  |         Type: | string |
  | ------------: | ------ |
  |      Default: | null   |
  | Valid Values: |        |
  |   Importance: | low    |

- #### ssl.trustmanager.algorithm

  SSL 커넥션에서 trust 매니저 팩토리가 사용할 알고리즘. 기본값은 자바 가상 머신에 설정된 trust 매니저 팩토리 알고리즘이다.

  |         Type: | string |
  | ------------: | ------ |
  |      Default: | PKIX   |
  | Valid Values: |        |
  |   Importance: | low    |
