# Microbiome WGS Analysis Pipeline — Study Edition


본 저장소는 **대장암(colorectal cancer) 포함 미생물군집 WGS 분석**을 공부 목적으로 정리한 레포입니다.

## What’s Inside
- `docs/`: 이론 및 단계별 가이드 (QC → Host 제거 → Taxonomy → Function → 통계/시각화)
- `pipeline/`: Snakemake 스켈레톤 + conda 환경 파일(실습 보조)
- `example_data/`: 예시 샘플 시트(공개 SRA를 사용할 것을 권장)

## Quick Start (요약)
1) **conda/mamba 설치**: `docs/00_install_conda.md` 참조
2) 환경 생성: `mamba env create -f pipeline/envs/base.yaml`
3) Snakemake 테스트: `snakemake --cores 4 -n` (드라이런)
4) 단계별 학습: `docs/01_workflow_overview.md`부터 차례로 읽기


## 추천 학습 순서
1. 워크플로우 개요 → 2. QC → 3. Host 제거 → 4. Taxonomic → 5. Functional → 6. 통계/모델 → 7. 시각화 → 8. 재현성/DB 버전 관리


## 면책
- 실제 임상 데이터 사용 시 IRB/동의/비식별화를 반드시 준수하세요.
- 데이터베이스/툴 버전에 따라 결과가 달라질 수 있습니다.
