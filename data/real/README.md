# 실측 데이터 (라즈베리파이)

스마트 분전반 AI 모니터링 시스템의 **실측** 1시간 요약입니다. 라즈베리파이가 매시 자동으로 올립니다.
가상 시뮬레이션 데이터(`data/*.csv`)와 섞이지 않게 이 폴더에만 씁니다.

- 계측: PZEM-004T(주 MCCB: 전압·전류·전력·전력량·역률·주파수) + SCT-013-030 ×3(분기 전류)
- 측정 5초 → 1분 집계(로컬 SQLite) → 1시간 요약(이 파일)
- 시설 대응(홍성 사무실): CT2 → c1 조명A, CT3 → c8 동력(환기팬모터), CT1 → c9 예비회로

| 열 | 뜻 |
|---|---|
| datetime | 1시간 구간 시작(KST) |
| total_load_kw / total_current_a / supply_voltage_v | 주 MCCB 유효전력·전류·전압 평균 (가상 데이터와 같은 이름) |
| voltage_min_v / voltage_max_v / current_max_a / power_avg_w / power_max_w | 주 MCCB 구간 최소·최대·평균 |
| energy_wh_hour | 그 1시간 사용 전력량(Wh, 누적값 차이) |
| pf_avg / frequency_avg_hz | 역률·주파수 평균 |
| unmeasured_avg_a | 미계측 전류(추정) = 주 전류 − 분기 CT 합 |
| ctN_current_a / ctN_max_a / ctN_load_pct_max | 분기 전류 평균·최대(A), 차단기 정격 대비 최대 부하율(%) |
| minutes | 그 시간 안에 저장된 1분 집계 수(60이면 빠짐 없음) |
| errors | 측정 오류 레코드 수 |
| status | ok(정상) / partial(빠진 분 있음 — 오류·범위 밖 값 제외 포함) |

배선 전 시험용 가상 값(mock)은 올리지 않습니다.
