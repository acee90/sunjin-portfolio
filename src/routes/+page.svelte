<script>
	import { gsap } from 'gsap';
	import { ScrollTrigger } from 'gsap/ScrollTrigger';

	gsap.registerPlugin(ScrollTrigger);

	// Svelte 5 바인딩을 사용하여 DOM 요소 참조
	let track = $state();
	let container = $state();

	// $effect는 의존성이 변경될 때마다 실행됩니다
	$effect(() => {
		// track과 container가 모두 바인딩되면 GSAP 설정
		if (!track || !container) return;

		const panels = gsap.utils.toArray('.panel');

		const ctx = gsap.to(track, {
			xPercent: -80,
			// 	 만약 xPercent: -100%라면:
			//   - track이 500vw만큼 왼쪽으로 이동
			//   - 그러면 track의 끝부분이 뷰포트 왼쪽 경계에 와서
			//   - 아무것도 보이지 않게 됩니다!
			ease: 'none', // scrub을 사용할 땐 'none'이 자연스럽습니다.

			scrollTrigger: {
				// 1. 트리거 대상 (이 섹션이 고정됩니다)
				trigger: container, // 바인딩된 요소 직접 사용

				// 2. 고정(pin) 활성화
				pin: true,

				// 3. 스크롤 연동
				scrub: 1,

				// 4. 시작/끝 지점
				start: 'top top',

				// 스크롤이 얼마나 지속될지 결정
				// track의 실제 너비에서 뷰포트를 뺀 값 = 실제로 이동해야 할 거리
				end: () => '+=' + (track.offsetWidth - window.innerWidth),

				markers: true // 개발용 마커 (배포 시 제거)
			}
		});

		// 클린업: 컴포넌트가 언마운트되면 ScrollTrigger 제거
		return () => {
			ctx.scrollTrigger?.kill();
		};
	});
</script>

<section class="section section-1">
	<h1>첫 번째 섹션</h1>
	<p>여기는 일반 세로 스크롤 영역입니다.</p>
	<p>아래로 스크롤하세요.</p>
</section>

<section class="panels-container" bind:this={container}>
	<div class="panels-track" bind:this={track}>
		<div class="panel panel-1">패널 1</div>
		<div class="panel panel-2">패널 2</div>
		<div class="panel panel-3">패널 3</div>
		<div class="panel panel-4">패널 4</div>
		<div class="panel panel-5">패널 5</div>
	</div>
</section>

<section class="section section-3 bg-green">
	<h1>세 번째 섹션</h1>
	<p>가로 스크롤이 모두 끝나면</p>
	<p>다시 일반 세로 스크롤이 시작됩니다.</p>
</section>

<style>
	.section {
		height: 100vh;
		display: grid;
		place-items: center;
		text-align: center;
	}
	.section-1 {
		background-color: #f0f0f0;
	}
	.section-3 {
		background-color: #f0f0f0;
	}

	/* 'pin' 될 섹션.
    뷰포트 크기와 정확히 일치해야 하며,
    내부 'track'이 넘칠 수 있도록 overflow: hidden 처리를 합니다.
  */
	.panels-container {
		height: 100vh;
		width: 100vw;
		overflow: hidden;
	}

	/* 패널들을 가로로 배치할 트랙 */
	.panels-track {
		height: 100%;
		display: flex;
		width: 500vw;
		will-change: transform; /* 애니메이션 성능 최적화 */
		/* 트랙의 오른쪽 끝 표시 */
		position: relative;
	}

	.panel {
		height: 100%;
		width: 100vw;
		flex-shrink: 0; /* flex 컨테이너에서 크기 축소 방지 */
		display: grid;
		place-items: center;
		font-size: 3rem;
		color: white;
	}

	.panel-1 {
		background-color: #61a0af;
	}
	.panel-2 {
		background-color: #ff9a8d;
	}
	.panel-3 {
		background-color: #6a6a6a;
	}
	.panel-4 {
		background-color: #3b7696;
	}

	.panel-5 {
		background-color: burlywood;
	}
</style>
