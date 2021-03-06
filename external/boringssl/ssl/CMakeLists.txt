include_directories(../include)

add_subdirectory(pqueue)

set(
  ssl_objects_dependencies
  $<TARGET_OBJECTS:pqueue>
  PARENT_SCOPE
)

add_library(
  ssl-objects OBJECT

  custom_extensions.c
  handshake_server.c
  handshake_client.c
  d1_both.c
  d1_lib.c
  d1_meth.c
  d1_pkt.c
  d1_srtp.c
  dtls_record.c
  s3_both.c
  s3_enc.c
  s3_lib.c
  s3_meth.c
  s3_pkt.c
  ssl_aead_ctx.c
  ssl_asn1.c
  ssl_buffer.c
  ssl_cert.c
  ssl_cipher.c
  ssl_ecdh.c
  ssl_file.c
  ssl_lib.c
  ssl_rsa.c
  ssl_session.c
  ssl_stat.c
  t1_enc.c
  t1_lib.c
  tls_record.c
)

add_library(
  ssl

  custom_extensions.c
  handshake_server.c
  handshake_client.c
  d1_both.c
  d1_lib.c
  d1_meth.c
  d1_pkt.c
  d1_srtp.c
  dtls_record.c
  s3_both.c
  s3_enc.c
  s3_lib.c
  s3_meth.c
  s3_pkt.c
  ssl_aead_ctx.c
  ssl_asn1.c
  ssl_buffer.c
  ssl_cert.c
  ssl_cipher.c
  ssl_ecdh.c
  ssl_file.c
  ssl_lib.c
  ssl_rsa.c
  ssl_session.c
  ssl_stat.c
  t1_enc.c
  t1_lib.c
  tls_record.c

  $<TARGET_OBJECTS:pqueue>
)

target_link_libraries(ssl crypto)

if(ENABLE_TESTS)
add_executable(
  ssl_test

  ssl_test.cc

  $<TARGET_OBJECTS:test_support>
)

target_link_libraries(ssl_test ssl crypto)
add_dependencies(all_tests ssl_test)
endif()
