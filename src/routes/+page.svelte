<script>
	import { onMount } from 'svelte';
	import { gsap } from 'gsap';
	import { ScrollTrigger } from 'gsap/ScrollTrigger';

	// 1. 플러그인 등록
	gsap.registerPlugin(ScrollTrigger);

	onMount(() => {
		// 2. onMount 내부에서 ScrollTrigger 설정
		gsap.to('.box', {
			x: 500, // 스크롤이 다 내려갔을 때 x 위치
			ease: 'none', // 'scrub'을 쓸 때는 'none'으로 해야 부드럽습니다.
			scrollTrigger: {
				trigger: '.section-wrapper', // 애니메이션이 일어날 전체 영역
				start: 'top top', // "영역의 top"이 "뷰포트의 top"에 닿을 때 시작
				end: 'bottom bottom', // "영역의 bottom"이 "뷰포트의 bottom"에 닿을 때 끝
				
				// ⬇️ 이 부분이 핵심입니다!
				scrub: true, // 스크롤 위치에 애니메이션을 1:1로 묶습니다. (true 또는 1, 2 등 숫자로 부드러움 조절 가능)
				
				markers: true // 개발용 마커 (배포 시 제거)
			}
		});
	});
</script>

<div class="section-wrapper">
	<div class="box">
		➡️
	</div>
</div>

<div style="height: 100vh; background-color: #eee;"></div>
<div style="height: 100vh;"></div>

<style>
	/* 스크롤 영역을 고정(pin)하지 않으면 스크롤과 함께 요소가 위로 올라가 버립니다. */
	/* 여기서는 간단한 예시를 위해 wrapper의 높이를 지정합니다. */
	.section-wrapper {
		height: 200vh; /* 스크롤할 수 있는 넉넉한 높이 (pin을 안 쓸 경우) */
		padding-top: 100px;
		overflow-x: hidden; /* 가로 스크롤바 방지 */
	}

	.box {
		width: 100px;
		height: 100px;
		background-color: royalblue;
		color: white;
		display: grid;
		place-items: center;
		font-size: 2rem;
	}

	body {
		margin: 0;
	}
</style>