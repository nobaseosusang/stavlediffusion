# Stable Diffusion with 2D Game Asset Generator API

**작품 개략**

이 프로젝트는 Stable Diffusion 모델을 구현한 FastAPI 백엔드 애플리케이션입니다. 사용자는 텍스트 프롬프트를 입력하여 이미지를 생성할 수 있으며, 이미지와 프롬프트를 기반으로 새로운 이미지를 생성할 수도 있습니다. 프롬프트에 "2D game asset" 키워드를 추가하여 2D 게임 에셋을 생성할 수 있습니다.

**기획 의도**

이 프로젝트는 stable diffusion이 그래픽카드가 있는 장치에서만 실행 되기에 그래픽카드가 없는 노트북 사용자들이 api를 활용해 이를 이용할 수 있도록 하기 위해 제작되었습니다. 성공적으로 배포할 경우 퍼블릭 ip에 post 요청을 보냄으로써 기능을 활용할 수 있을 것입니다.

**구현 전략**

**자랑하고 싶은 점**



## 요구 사항

- Python 3.7 이상
- pip
- 하드웨어에 NVDIA 그래픽카드가 있을 것(배포를 실패해서,,)

## 설치 방법

1. **저장소 클론**

    ```bash
    git clone https://github.com/yourusername/stable-diffusion-2d-game-asset-generator.git
    cd stable-diffusion-2d-game-asset-generator
    ```

2. **가상 환경 설정 및 활성화**

    ```bash
    python -m venv venv
    source venv/bin/activate  # Linux/Mac
    .\venv\Scripts\activate  # Windows
    ```

3. **필요한 패키지 설치**

    ```bash
    pip install -r requirements.txt
    ```

## 환경 변수 설정

1. `.env` 파일을 프로젝트 루트 디렉토리에 생성하고, Hugging Face API 토큰을 추가합니다.

    ```
    HF_TOKEN=your_huggingface_token
    ```

## FastAPI 애플리케이션 실행

```bash
uvicorn main:app --reload --host 0.0.0.0 --port 8000
```

## API 엔드포인트

**1. 기본 엔드포인트**
GET /

서버 상태를 확인할 수 있습니다.
```
Request:

bash
 
curl http://localhost:8000/
Response:

json
 
{
    "message": "Stable Diffusers API에 오신 것을 환영합니다"
}
```
**2. 이미지 생성 엔드포인트**
POST /api/generate/

입력된 프롬프트를 사용하여 이미지를 생성합니다.

```
Request:

json
 
{
    "prompt": "A fantasy landscape with mountains and rivers",
    "seed": 42,
    "num_inference_steps": 30,
    "guidance_scale": 7.5,
    "model_name": "CompVis/stable-diffusion-v1-4"
}
Response:

이미지 파일 (image/png)
```

**3. 2D 게임 에셋 생성 엔드포인트**
POST /api/generate_2d_asset/

입력된 프롬프트에 "2D game asset" 키워드를 추가하여 2D 게임 에셋을 생성합니다.

```
Request:

json
 
{
    "prompt": "A beautiful forest",
    "seed": 42,
    "num_inference_steps": 30,
    "guidance_scale": 7.5,
    "model_name": "CompVis/stable-diffusion-v1-4"
}
Response:

이미지 파일 (image/png)
```

**4. 이미지 변환 엔드포인트 (img2img)**
POST /api/img2img/

업로드된 이미지를 기반으로 새로운 이미지를 생성합니다.

```
Request:

파일: 업로드할 이미지 파일
JSON 데이터:
json
 
{
    "prompt": "A cyberpunk cityscape at night",
    "seed": 42,
    "num_inference_steps": 30,
    "guidance_scale": 7.5,
    "model_name": "CompVis/stable-diffusion-v1-4"
}
Response:

이미지 파일 (image/png)
```

**5. 이미지 생성 엔드포인트(배경 제거)**
POST /api/generate_withoutbg/

2번과 동일하지만 배경을 삭제합니다.

```
Request:

json
 
{
    "prompt": "A fantasy landscape with mountains and rivers",
    "seed": 42,
    "num_inference_steps": 30,
    "guidance_scale": 7.5,
    "model_name": "CompVis/stable-diffusion-v1-4"
}
Response:

이미지 파일 (image/png)
```