![logo](https://raw.githubusercontent.com/ProtossDragoon/PlankHyundong/944c38802cfe392ed6ed194ccca6a083563add45/docs/images/logo.svg)

<br>

<div align="center">

[![Hits](https://hits.seeyoufarm.com/api/count/incr/badge.svg?url=https%3A%2F%2Fgithub.com%2FProtossDragoon%2FPlankHyundong&count_bg=%23FFA217&title_bg=%2345FFDE&icon=&icon_color=%23E7E7E7&title=hits&edge_flat=false)](https://hits.seeyoufarm.com) 

</div>

<br>

# 플랭크현동 가이드라인

이 문서는 [README.md](https://github.com/ProtossDragoon/PlankHyundong/blob/main/README.md) 가 다루지 못한 구체적인 내용을 포함하고 있습니다.

## 결과물

<table>
<thead align="center">
  <tr>
    <th>원본</th>
    <th>중간 결과물</th>
    <th>최종 결과물</th>
  </tr>
</thead>
<tbody align="center">
  <tr>
    <th><img width="250" src="https://github.com/ProtossDragoon/PlankHyundong/blob/docs/docs/images/hyundong360_snapshot.jpg"></td></th>
    <td><img width="250" src="https://github.com/ProtossDragoon/PlankHyundong/blob/docs/docs/images/figure_middle_collage.png"></td>
    <td><img width="250" src="https://github.com/ProtossDragoon/PlankHyundong/blob/docs/docs/images/figure_final_collage.jpg"></td>
  </tr>
  <tr>
    <th><img width="250" src="https://github.com/ProtossDragoon/PlankHyundong/blob/c466d902d2ec4d276452b78fdf258d2e73a0da13/docs/images/collecting_video.gif"></th>
    <td><img width="250" src="https://github.com/ProtossDragoon/PlankHyundong/blob/docs/docs/images/hyundong360.gif"></td>
    <td><img width="250" src="https://github.com/ProtossDragoon/PlankHyundong/blob/docs/docs/images/hyundong360_removebg.gif"></td>
  </tr>
  <tr>
    <td></td>
    <td>2022년 8월 9일</td>
    <td>2022년 8월 24일</td>
  </tr>
</tbody>
</table>

# 목차

- [구성요소별 디테일](#steps)
    - [피사체 동영상 촬영하기](#step1)
      - [촬영 권장사항](#step1-1)
      - [촬영 주의사항](#step1-2)
      - [촬영 권장 및 주의사항 관련 실험](#step1-experiment)
    - [비디오로부터 이미지 샘플링하기](#step2)
    - [이미지에 대한 카메라 포즈 구하기](#step3)
    - [NeRF 모델 학습시키기](#step4)
      - [학습 옵션](#step4-1)
        - [학습 옵션 관련 실험](#step4-1-experiment)
    - [NeRF 모델로부터 Mesh 만들고 다듬기](#step5)
      - [Mesh 만들기](#step5-1)
        - [Mesh Renderer 파라미터 실험](#step5-1-experiment)
      - [Mesh 다듬기](#step5-2)
    - [피규어 인쇄 및 후가공하기](#step6)
      - [피규어 인쇄하기](#step6-1)
        - [3D 프린터 옵션 실험](#step6-1-experiment)
      - [인쇄된 피규어 후가공하기](#step6-2)
- [평가](#evaluation)
- [도와주세요](#todo)
- [팀과 메이커로그](#team)

<a name="steps"></a>
# 구성요소별 디테일

![파이프라인](https://github.com/ProtossDragoon/PlankHyundong/blob/docs/docs/images/pipeline.png )

<table style="table-layout: fixed; width: 100%;">
<thead align="center" >
  <tr>
    <th>step</th>
    <th>1️⃣</th>
    <th>2️⃣</th>
    <th>3️⃣</th>
  </tr>
</thead>
<tbody align="center">
  <tr>
    <td>output</td>
    <td>RGB 비디오</td>
    <td>이미지와 포즈</td>
    <td>뉴럴넷 기반 3d 표현</td>
  </tr>
  </tr>
    <td></td>
    <td><img width="230" src=https://github.com/ProtossDragoon/PlankHyundong/blob/docs/docs/images/non_forward_facing.gif></td>
    <td><img width="230" src=https://github.com/ProtossDragoon/PlankHyundong/blob/docs/docs/images/wandb_show_pose.gif></td>
    <td><img width="230" src=https://github.com/ProtossDragoon/PlankHyundong/blob/docs/docs/images/wandb_visualize_implicit_representation.gif></td>
  </tr>
</tbody>
</table>

<table style="table-layout: fixed; width: 100%;">
<thead align="center">
  </tr>
    <th>step</th>
    <th>4️⃣</th>
    <th>5️⃣</th>
    <th>6️⃣</th>
  </tr>
</thead>
<tbody align="center">
  <tr>
    <td>output</td>
    <td>메쉬가 적용된 3d 표현</td>
    <td>슬라이서 소프트웨어</td>
    <td>결과물 피규어</td>
  </tr>
  <tr>
    <td></td>
    <td><img width="230" src=https://github.com/ProtossDragoon/PlankHyundong/blob/docs/docs/images/meshed_representation.gif></td>
    <td><img width="230" src=https://github.com/ProtossDragoon/PlankHyundong/blob/docs/docs/images/slicer_sw.gif></td>
    <td><img width="230" src=https://github.com/ProtossDragoon/PlankHyundong/blob/docs/docs/images/result_1.png></td>
  </tr>
</tbody>
</table>

<a name="step1"></a>
## 피사체 동영상 촬영하기

<a name="step1-1"></a>
### 촬영 권장사항

<table>
<thead align="center">
  <tr>
    <th>권장, 360도 촬영</th>
    <th>정면촬영 (Forward Facing)</th>
  </tr>
</thead>
<tbody align="center">
  <tr>
    <td><img src=https://github.com/ProtossDragoon/PlankHyundong/blob/docs/docs/images/non_forward_facing.gif></td>
    <td><img src=https://github.com/Fyusion/LLFF/raw/master/imgs/capture.gif></td>
  </tr>
  <tr>
    <td>이 프로젝트에서 사용한 방법</td>
    <td>모델 학습은 가능하지만 피규어를 제작할 수 없음. 동영상 출처: <a href="https://github.com/Fyusion/LLFF">Google LLFF</a></td>
  </tr>
</tbody>
</table>

- ✅ 충분한 조명을 확보하여 충분히 짧은 셔터 속도를 사용할 수 있도록 준비합니다.
- ✅ 피사체를 가운데에 두고 촬영자는 360도로 돌면서 촬영합니다.
- ✅ 다양한 각도를 수집하기 위해 위 아래로 S자를 만들면서 촬영합니다.
- ✅ 각 각도에 대한 이미지를 동일하게 수집하기 위해 일정한 속도로 돌며 촬영합니다.
- ✅ NeRF 의 설계에는 동적인 물체가 고려되지 않았으므로 피사체의 움직임을 최소화합니다.

<a name="step1-2"></a>
### 촬영 주의사항

<table>
<thead align="center">
  <tr>
    <th>번들거리는 물체가 등장</th>
    <th>움직이는 신체가 등장</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td align="center"><img src=https://github.com/ProtossDragoon/PlankHyundong/blob/docs/docs/images/worse_practice_1.jpeg alt=""></td>
    <td align="center"><img src=https://github.com/ProtossDragoon/PlankHyundong/blob/docs/docs/images/worse_practice_2.png alt=""></td>
  </tr>
</tbody>
</table>

- ❗ 피사체 주변에는 번들거리는 물체가 없도록 주의합니다.
    - 실험을 통해 피사체 주변에 차가 많을 때 결과가 좋지 않음을 확인했습니다.
- ❗ 피사체를 제외한 주변의 움직이는 사물이나 그림자 등이 등장하지 않도록 주의합니다.
    - 실험을 통해 촬영자의 팔이 나온 데이터를 제거했을 때 성능이 매우 향상됨을 확인했습니다.

<a name="step1-experiment"></a>
### 촬영 권장 및 주의사항 관련 실험

![wandb_experiment](https://github.com/ProtossDragoon/PlankHyundong/blob/docs/docs/images/wandb_experiment.gif)

이와 관련된 실험으로부터 얻은 인사이트는 [wandb 리포트](https://wandb.ai/plank-hyundong/plank-hyundong/reports/Hyperparameter-Experiment-Ablation-Study--VmlldzoyNDAzMDYz)에서 모두 확인할 수 있습니다.

<a name="step2"></a>
## 비디오로부터 이미지 샘플링하기

<p style="text-align:center;">
<a href="https://colab.research.google.com/github/ProtossDragoon/PlankHyundong/blob/main/notebooks/sampling_colab.ipynb">
  <img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/>
</a></p>

|   파라미터    |  설명  |
|:-----------:|:--------------:|
| `dir_path`  | 비디오 파일의 경로 |
| `frame`     | 비디오로부터 샘플링되는 이미지의 개수 |

스크립트를 이용하여 촬영한 비디오를 이미지로 등간격 샘플링합니다.

- ✅ 카메라 트래젝토리가 길다면 더 잘게 잘라 주는 것이 좋습니다.
- ❗ 카메라 트래젝토리가 짧고 렌즈를 열어두는 시간이 짧은 경우, 동영상으로부터 이미지를 너무 잘게 샘플링한다면 성능에 악영향을 미칠 수 있습니다.

<a name="step3"></a>
## 이미지에 대한 카메라 포즈 구하기

<p style="text-align:center;">
<a href="https://colab.research.google.com/github/ProtossDragoon/PlankHyundong/blob/main/notebooks/colmap_colab.ipynb">
  <img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/>
</a></p>

**NOTE:** 반드시 GPU 런타임을 사용해야 합니다.

NeRF 의 입력은 (이미지, 카메라포즈) 의 집합입니다. 커스텀 이미지로부터 이미지 각각에 해당하는 카메라 포즈를 계산하기 위해 [COLMAP](https://github.com/colmap/colmap)을 기반으로 동작하는 [LLFF](https://github.com/Fyusion/LLFF) 저자의 스크립트를 사용합니다. 하지만 LLFF 스크립트를 구동할 수 있는 환경을 구축하는 일은 꽤 까다롭습니다. 이러한 문제를 피하기 위해 [플랭크현동이 제공하는 노트북](https://github.com/ProtossDragoon/PlankHyundong/blob/main/notebooks/colmap_colab.ipynb)을 사용하세요. COLAB 클라우드 컴퓨터에서 모든 연산이 이루어집니다. 실행이 완료되면 데이터셋 폴더 안에 NeRF 모델을 실행시키는 데 필요한 `poses_bounds.npy` 파일이 생성됩니다.

<a name="step4"></a>
## NeRF 모델 학습시키기

<p style="text-align:center;">
<a href="https://colab.research.google.com/github/ProtossDragoon/PlankHyundong/blob/main/notebooks/nerf_wandb_colab.ipynb">
  <img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/>
</a></p>

**NOTE:** 반드시 GPU 런타임을 사용해야 합니다.

<a name="step4-1"></a>
### 학습 옵션

|       옵션       |  파라미터 | 역할 |
|:---------------:|:------:|:---:|
| `--wandbproject`                      | wandb 프로젝트명      | 본 프로젝트에서는 필요한 Metric, 평가지표들을 시각화하기 위하여 실험 관리 도구인 wandb를 사용합니다.|
| `--wandbentity`                       | wandb 팀명 또는 유저명 | 본 프로젝트에서는 필요한 Metric, 평가지표들을 시각화하기 위하여 실험 관리 도구인 wandb를 사용합니다.|
| `--no_ndc`, `--spherify`, `--lindisp` |                    | forward facing scene 에서는 필요하지 않지만, 360 scene 에 대해서는 반드시 사용해야 하는 플래그입니다.|

<a name="step4-1-experiment"></a>
#### 학습 옵션 관련 실험

![wandb_experiment](https://github.com/ProtossDragoon/PlankHyundong/blob/docs/docs/images/wandb_experiment.gif)

이와 관련된 실험으로부터 얻은 인사이트는 [wandb 리포트](https://wandb.ai/plank-hyundong/plank-hyundong/reports/Hyperparameter-Experiment-Ablation-Study--VmlldzoyNDAzMDYz)에서 모두 확인할 수 있습니다.

<a name="step5"></a>
## NeRF 모델로부터 Mesh 만들고 다듬기

<a name="step5-1"></a>
### Mesh 만들기

<p style="text-align:center;">
<a href="https://colab.research.google.com/github/ProtossDragoon/PlankHyundong/blob/main/notebooks/extract_mesh_colab.ipynb">
  <img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/>
</a></p>

**NOTE:** 반드시 GPU 런타임을 사용해야 합니다.

NeRF 모델로 학습시킨 학습시킨 모델을 로드한 뒤, `PyMCubes` 패키지를 통해 표면(iso-surface)을 추출하고 그 결과물인 `3d.obj` 파일을  저장하는 단계입니다. 이 노트북의 출처는 [NeRF 공식 저장소](https://github.com/bmild/nerf/blob/master/extract_mesh.ipynb)입니다.
 
- 위 노트북에서는 학습된 NeRF 모델의 3D 표현(implicit representation)을 시각화 하기 위해 `pyrender` 을 이용해 `turntable.mp4` 영상을 생성합니다.
- `trimesh` 가 적용된 3D 표현을 실시간으로 미리보기할 수 있습니다. 
- `N` 과 `threshold` 변수값 조절을 통해 추출한 결과물의 퀄리티 변화를 확인할 수 있습니다.

<a name="step5-1-experiment"></a>
### Mesh Renderer 파라미터 실험

| param      |       role       | 실험값<br>(채택값: ✔️) |
|:----------:|:---------------:|:-------------:|
| threshold  | threshold 값이 작으면 파티클의 밀도가 적은 공간에서도 mesh 를 생성합니다.<br>높을수록 용량이 감소합니다. | 50, **100✔️** |
| N          | 쉽게 말해 해상도값입니다.<br>높을수록 용량이 증가합니다. | 256, **512✔️** |

- 표면(iso-surface)을 추출할 때 파라미터 `threshold` 와 `N` 값의 미세소정을 통해 결과물의 성능을 향상시킬 수 있습니다.
- 플랭크현동 프로젝트에서는 결과물의 퀄리티 및 GPU, 메모리 등의 리소스를 고려하여 이상적인 파라미터(threshold=100, N=512)를 채택했습니다.

<a name="step5-2"></a>
### Mesh 다듬기

우리가 관심있는 피사체 외 만들어진 3D 표현 잡음들을 제거하기 위해 수작업이 필요합니다.

<table>
<thead align="center">
  <tr>
    <th>누끼를 따지 않은 이미지를<br> 사용하는 경우</th>
    <th>누끼를 딴 이미지를<br> 사용하는 경우</th>
  </tr>
</thead>
<tbody align="center">
  <tr>
    <td><img width="320" src="https://github.com/ProtossDragoon/PlankHyundong/blob/docs/docs/images/trim_mesh.png" alt=""></td>
    <td><img width="320" src="https://github.com/ProtossDragoon/PlankHyundong/blob/docs/docs/images/trim_mesh_case_without_background.jpg" alt=""></td>
  </tr>
  <tr>
    <td>바닐라 NeRF 는 피사체와 배경을 분리하지 못합니다. 따라서 NeRF 모델을 이용해 생성한 3D 표현애는 피사체 주변의 바닥, 근처 장애물 등이 포함됩니다. 따라서 현실에서 직접 취득한 데이터를 그대로 사용하는 경우 수작업에 많은 시간이 필요할 수 있습니다.</td>
    <td>만약 동영상으로부터 샘플링한 이미지들에서 누끼를 제거해 사용했다면, 왼쪽과 같은 문제를 조금 덜어낼 수 있습니다. 누끼가 제거된 이미지들로 NeRF 모델을 학습한 경우 수작업으로 제거해야 할 피사체 외 잡음들이 많이 사라지기 때문입니다.</td>
  </tr>
</tbody>
</table>

<a name="step6"></a>
## 피규어 인쇄 및 후가공하기

<a name="step6-1"></a>
### 피규어 인쇄하기

`.obj` 파일을 타깃 프린터가 호환되는 슬라이서 프로그램에 업로드하여 출력하는 단계입니다. 예를 들어, 사용할 프린터가 3DWOX(DP203) 인 경우, 대표적으로 사용할 수 있는 슬라이서 프로그램은 Sindoh 슬라이서입니다.

<table>
<thead align="center">
  <tr>
    <th>3D 프린터</th>
    <th>슬라이서 프로그램</th>
    <th>출력 준비작업</th>
  </tr>
</thead>
<tbody align="center">
  <tr>
    <td>3DWOX1(DP203)</td>
    <td><a ref="https://www.sindoh.com/downcenter/dc_comSearch.do">Sindoh 슬라이서</a></td>
    <td>서포트, 내부 채움, 파라미터 설정 등</td>
  </tr>
  <tr>
    <td><img width="200" src="https://github.com/ProtossDragoon/PlankHyundong/blob/docs/docs/images/printer_3DWOX1.png"></td>
    <td><img width="200" src="https://github.com/ProtossDragoon/PlankHyundong/blob/docs/docs/images/logo_sindoh.png"></td>
    <td><img width="200" src="https://github.com/ProtossDragoon/PlankHyundong/blob/docs/docs/images/waiting_for_printing.jpeg"></td>
  </tr>
</tbody>
</table>

<a name="step6-1-experiment"></a>
### 3D 프린터 옵션 실험

- 3D 프린터의 다양한 옵션에 따라 결과물의 퀄리티가 달라집니다.
- 3D 프린터의 결과물의 퀄리티에 가장 많은 영향을 미치는 요소는 레이어 높이, 출력 속도입니다.

|   |       옵션       | 레이어 높이 | 출력 속도 | 소요된 출력시간 | 정성평가 |
|:--:|:---------------:|:------:|:--------:|:----------:|:----:|
| 0️⃣  | 2022년 8월 9일 중간 결과물 | ???  |  ???  | ??  | worst |
| 1️⃣  | 데이터 정제           | 0.1mm |  20mm/s | 4h  | |
| 2️⃣  | 데이터 정제           | 0.1mm |  40mm/s | 4h  | |
| 3️⃣  | 데이터 정제           | 0.2mm |  20mm/s | 3h  | |
| 4️⃣  | 데이터 정제           | 0.2mm |  40mm/s | 3h  | |
| 5️⃣  | 데이터 정제 + 누끼 제거 | 0.1mm |  20mm/s | 17h | best |
| 6️⃣  | 데이터 정제 + 누끼 제거 | 0.1mm |  40mm/s | 14h | |
| 7️⃣  | 데이터 정제 + 누끼 제거 | 0.2mm |  20mm/s | 9h  | |
| 8️⃣  | 데이터 정제 + 누끼 제거 | 0.2mm |  40mm/s | 7h  | |

> **옵션이 데이터 정제(1️⃣, 2️⃣, 3️⃣, 4️⃣), 데이터 정제 + 누끼제거 (5️⃣, 6️⃣, 7️⃣, 8️⃣) 두 가지인 이유?** 누끼를 제거한 데이터셋은 배경이 제거되면서 PSNR과 loss에 영향을 미치기 때문에 정량적인 평가가 불가능합니다. 단순한 시각화만으로는 두 결과물에 대한 정성적인 평가가 어려웠습니다. 따라서 두 경우 모두에 대해 실제 피규어를 인쇄해본 뒤 이들을 비교했습니다.

<table style="table-layout: fixed; width: 100%;">
<thead align="center" >
  <tr>
    <th> 0️⃣ 2022년 8월 9일 중간 결과물 </th>
  </tr>
</thead>
<tbody align="center">
  <tr>
    <td><img width="300" src="https://github.com/ProtossDragoon/PlankHyundong/blob/docs/docs/images/figure_middle_collage.png"></td>
  </tr>
</tbody>
</table>

<table style="table-layout: fixed; width: 100%;">
<thead align="center" >
  <tr>
    <th> 결과물 </th>
    <th> 1️⃣ 2️⃣ 3️⃣ 4️⃣ </th>
    <th> 5️⃣ 6️⃣ 7️⃣ 8️⃣ </th>
  </tr>
</thead>
<tbody align="center">
  <tr>
    <td>정면</td>
    <td><img width="300" alt="1234_ff" src="https://github.com/ProtossDragoon/PlankHyundong/blob/docs/docs/images/result_1234_ff.jpg"></td>
    <td><img width="300" alt="5678_ff" src="https://github.com/ProtossDragoon/PlankHyundong/blob/docs/docs/images/result_5678_ff.jpg"></td>
  </tr>
  <tr>
    <td>후면</td>
    <td><img width="300" alt="1234_back" src="https://github.com/ProtossDragoon/PlankHyundong/blob/docs/docs/images/result_1234_back.jpg"></td>
    <td><img width="300" alt="5678_back" src="https://github.com/ProtossDragoon/PlankHyundong/blob/docs/docs/images/result_5678_back.jpg"></td>
  </tr>
  <tr>
    <td>측면</td>
    <td><img width="300" alt="1234_side" src="https://github.com/ProtossDragoon/PlankHyundong/blob/docs/docs/images/result_1234_side.jpg"></td>
    <td><img width="300" alt="5678_side" src="https://github.com/ProtossDragoon/PlankHyundong/blob/docs/docs/images/result_5678_side.jpg"></td>
  </tr>
</tbody>
</table>

- 특히 레이어높이 옵션을 변경하면 출력물의 정교함을 조절할 수 있습니다.
- 출력속도가 느리면 출력물 중간중간 거미줄같은 잔해가 생기는 현상이 나타날 수 있습니다.

<table style="table-layout: fixed; width: 100%;">
<thead align="center" >
  <tr>
    <th> 1️⃣ 과 3️⃣ 의 손 비교 </th>
    <th> 1️⃣ 3️⃣ 5️⃣ 7️⃣ 의 거미줄 현상</th>
  </tr>
</thead>
<tbody align="center">
  <tr>
    <td><img width="300" src="https://github.com/ProtossDragoon/PlankHyundong/blob/docs/docs/images/printer_experiment_hand.png"></td>
    <td><img width="300" src="https://github.com/ProtossDragoon/PlankHyundong/blob/docs/docs/images/printer_experiment_spider.png"></td>
  </tr>
</tbody>
</table>

<a name="step6-2"></a>
### 인쇄된 피규어 후가공하기

높은 퀄리티의 결과물을 얻기 위해서는 3D 프린팅 결과물을 후가공할 필요가 있습니다. 기본적으로는 서포트(혹은 라프트)등 구조물과 거미줄 등 미관을 해치는 요소들을 제거합니다. 사포질과 도색을 추가적으로 진행하기도 합니다.

<table>
<thead align="center">
  <tr>
    <th></th>
    <th>before</th>
    <th>after</th>
  </tr>
</thead>
<tbody align="center">
  <tr>
    <td>라프트 제거</td>
    <td><img width="300" src="https://github.com/ProtossDragoon/PlankHyundong/blob/docs/docs/images/figure_postprocessing_before.jpg"></td>
    <td><img width="300" src="https://github.com/ProtossDragoon/PlankHyundong/blob/docs/docs/images/figure_postprocessing_ongoing.jpg"></td>
  </tr>
</tbody>
</table>

<a name="evaluation"></a>
# 평가

- loss, PSNR 등의 정량적 metric 은 ‘3d Reconstruction 이 정말정말 잘 되었는가?' 를 판단할 수 없다고 생각했습니다.
- 이를 보완하기 위한 [정성적인 메트릭을 만들 필요](https://www.notion.so/janghoo/3D-e0ca0bd17dd447728b06c236e9abd56f)가 있었습니다.
- [구글 폼](https://docs.google.com/forms/d/e/1FAIpQLScj3vhJWWyFJM4KYGAUbpEiJMA9KHdTYpU5Q12IAYlCcFXeOg/viewform)으로 정량 평가를 모방했습니다.
- 목표치는 Accuracy 50% 이상이었습니다.

<table>
<thead align="center">
  <tr>
    <th></th>
    <th>Q1 - 인물 맞추기</th>
    <th>Q2 - 착의 맞추기</th>
  </tr>
</thead>
<tbody align="center">
  <tr>
    <td></td>
    <td><img width="300" src="https://github.com/ProtossDragoon/PlankHyundong/blob/docs/docs/images/evaluation_q2_1.png"></td>
    <td><img width="300" src="https://github.com/ProtossDragoon/PlankHyundong/blob/docs/docs/images/evaluation_q1_1.jpg"></td>
  </tr>
  <tr>
    <td></td>
    <td><img width="300" src="https://github.com/ProtossDragoon/PlankHyundong/blob/docs/docs/images/evaluation_q2_2.png"></td>
    <td><img width="300" src="https://github.com/ProtossDragoon/PlankHyundong/blob/docs/docs/images/evaluation_q1_2.png"></td>
  </tr>
  <tr>
    <td>Accuracy</td>
    <td>47%</td>
    <td>54%</td>
  </tr>
</tbody>
</table>

<a name="todo"></a>
# 도와주세요

- [NeRF 이후의 연구 결과물](https://docs.google.com/spreadsheets/d/1l9NnZXEUVwPLEHnb81_gdXcD1DCXJUaR2RkeRIaMSo0/edit?usp=sharing) - 가령 동적 피사체에 대응할 수 있고 정교한 3D 표현을 만들어낼 수 있는 모델 - 들을 적용해보아야 합니다.
- 모델에 다양한 연산들을 추가하고 모델의 구조를 변경하여 바닐라 NeRF 모델의 성능을 뛰어넘는 결과를 만들어보아야 합니다.
- 파이프라인의 요소를 각각 별도의 노트북으로 분리한 상태로 관리하는 것이 아니라 파이프라인 요소들 각각을 명확히 이해하고 온전하게 연결해야 합니다.

<a name="team"></a>
# 팀과 메이커로그

- [세종대학교 인공지능 동아리 SAI](https://github.com/sju-coml/SAI)
- [프로젝트 칸반](https://www.notion.so/janghoo/21fcf2a58bd0412d98750e92156b728b?v=fb1550801bd94e748c1f13bc2c12c51b)
- 특히 유의미했던 고민들
  - [‘3D 화 한다’ 에 대한 명확한 기준 설정하기](https://www.notion.so/janghoo/3D-e0ca0bd17dd447728b06c236e9abd56f)

![team.jpeg](https://github.com/ProtossDragoon/PlankHyundong/blob/docs/docs/images/team.jpeg)

![logo-color.png](https://github.com/ProtossDragoon/PlankHyundong/blob/docs/docs/images/logo_background.png)
