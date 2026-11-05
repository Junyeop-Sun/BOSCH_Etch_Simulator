# BOSCH 식각 31→9 시뮬레이터

공정 센서 31개를 물리적으로 해석 가능한 9개로 정리하고, 평균 Si 식각 깊이·균일도·가장자리 차이 등 6개 출력을 보여주는 교육·탐색용 웹 UI입니다.

## 가장 빠르게 실행하기

`index.html`을 더블클릭하면 됩니다. 외부 서버나 인터넷 연결이 필요하지 않으며 모델과 화면 코드가 HTML 안에 포함돼 있습니다.

## 파일 설명

| 파일 | 역할 |
|---|---|
| `index.html` | 바로 공유하거나 GitHub Pages로 공개할 수 있는 완성 UI |
| `render_intuitive_dashboard.py` | HTML 화면을 다시 생성하는 Python 소스 |
| `simulator_bundle.json` | 학습된 Ridge 계수, 관측 범위, 시뮬레이터용 데이터 |
| `PARAMETER_31_TO_9.csv` | 31개 센서의 유지·통합·제거 근거 |
| `FINAL_9_PARAMETERS.csv` | 최종 9개 파라미터 정의 |
| `MULTIOUTPUT_MODEL_METRICS.csv` | LOLO MAE·RMSE·R² |
| `MULTIOUTPUT_OOF_PREDICTIONS.csv` | 각 웨이퍼의 실측값과 로트 제외 예측값 |
| `LOT_BETWEEN_WITHIN_DIAGNOSTICS.csv` | 로트 간·로트 내 변동 분해 |
| `GAS_MAPPING_VALIDATION.csv` | Gas4=C4F8, Gas5=SF6 추정 근거 |
| `advanced/build_final_dashboard.py` | 원자료부터 모델을 다시 학습하는 참고 코드 |

## UI 수정하기

Python 3.10 이상을 설치한 뒤 이 폴더에서 실행합니다.

```bash
python -m venv .venv

# Windows
.venv\Scripts\activate

pip install -r requirements.txt
python render_intuitive_dashboard.py
```

`render_intuitive_dashboard.py`를 수정한 후 다시 실행하면 `index.html`이 갱신됩니다. 색상과 배치는 `CSS`, 동작은 `JS`, 장비 그림은 `SVG`, 화면 구조는 `HTML` 문자열에서 수정할 수 있습니다.

`advanced/build_final_dashboard.py`는 원자료와 기존 분석 모듈이 있어야 실행됩니다. 공개 패키지에 원자료를 포함하지 않았다면 모델 재학습에는 사용할 수 없고, 분석 방법을 확인하기 위한 참고 코드로 사용합니다.

## GitHub에서 공동 작업하기

1. GitHub에서 새 저장소를 만듭니다.
2. 이 폴더 안의 파일을 저장소 최상위에 모두 업로드합니다.
3. 저장소를 공개하면 다른 사람이 코드를 읽고 Fork 또는 Pull Request로 수정을 제안할 수 있습니다.
4. 직접 수정 권한을 줄 사람은 저장소의 `Settings → Collaborators`에서 초대합니다.
5. 변경할 때는 `main`을 바로 수정하기보다 별도 브랜치에서 수정하고 Pull Request로 검토하는 방식을 권장합니다.

## GitHub Pages로 웹주소 만들기

1. 저장소에서 `Settings → Pages`로 이동합니다.
2. `Build and deployment`에서 `Deploy from a branch`를 선택합니다.
3. Branch는 `main`, 폴더는 `/ (root)`를 선택하고 저장합니다.
4. 잠시 후 `https://계정이름.github.io/저장소이름/` 주소가 생성됩니다.

`index.html`이라는 이름을 사용했기 때문에 별도 웹 빌드 과정 없이 바로 열립니다.

## 공유 전 확인할 사항

- `simulator_bundle.json`과 OOF CSV에는 원자료에서 계산된 파생 데이터가 포함됩니다. 회사·대회 규정상 공개 가능한지 먼저 확인해야 합니다.
- 공개 저장소에 올리기 전 사용할 라이선스를 정해야 합니다. 다른 사람이 수정·재배포하도록 허용하려면 MIT, Apache-2.0 같은 오픈소스 라이선스를 검토할 수 있습니다.
- 이 UI는 센서 MV 기반 연관 예측입니다. 장비 SV 레시피 추천이나 인과 검증 결과로 표현하면 안 됩니다.
