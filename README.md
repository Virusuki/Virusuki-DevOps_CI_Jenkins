#Jenkins Overview(CI)
- 개발자가 소스코드를 깃허브에 푸시하면 깃허브에 의해 젠킨스 파이프라인이 트리거가 되고, 궁극적으로 타겟 서버(Amazon EC2)에 워크로드를 배포하는 시나리오다.
- Docker-hub은 ECR registry를 활용함.

<img src="https://github.com/Virusuki/Virusuki-DevOps_CI_Jenkins/blob/main/img/jenkins%20overview(CI).jpg" width="600px" height="400px" title="px(픽셀) 크기 설정" alt="AWS의 아키텍처.jpg"></img><br/>


#AWS의 아키텍처
- AWS의 단일 VPC에 퍼블릭 서브넷과 프라이빗 서브넷으로 나뉘어 젠킨스는 프라이빗 서브넷에 위치하고, 젠킨스에 접근하기 위해 AWS의 ALB를 활용
- 개발자가 젠킨스 설정을 위해서 SSH 접근을 할때는 퍼블릭 서브넷에 있는 Bastion(EC2) 서버를 활용하고, 개발자는 bastion 서버에 퍼블릭로 ssh를 통한 IP에 접근하고 bastion 서버에서 젠킨스 서버로 ssh 접근을 통해서 젠킨스 서버를 설정함. 
- 그리고, 다른 개발자가 젠킨스에 접근할 수 있도록 퍼블릭 서브넷에 ALB를 활용해서 접근할 수 있도록 설정.

<img src="https://github.com/Virusuki/Virusuki-DevOps_CI_Jenkins/blob/main/img/AWS%EC%9D%98%20%EC%95%84%ED%82%A4%ED%85%8D%EC%B2%98.jpg" width="580px" height="550px" title="px(픽셀) 크기 설정" alt="AWS의 아키텍처"></img><br/>


#네트워크 아키텍처
- 단일 VPC에 퍼블릭 서브넷은 VPC 대역 외에는 인터넷게이트웨이로 라우트 설정.
- 프라이빗 서브넷은 VPC 대역 외에는 전부 NAT 대역으로 가서 인터넷 접근할 수 있도록 설정

<img src="https://github.com/Virusuki/Virusuki-DevOps_CI_Jenkins/blob/main/img/%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC%20%EC%95%84%ED%82%A4%ED%85%8D%EC%B2%98.jpg" width="580px" height="550px" title="px(픽셀) 크기 설정" alt="네트워크 아키텍처"></img><br/>
