<template>
<!DOCTYPE html>
<html lang="ko">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1">

    <title>TravelClub</title>

    <!-- favicons -->
    <link href="../assets/img/favicon.png" rel="icon">
    <link href="../assets/img/apple-touch-icon.png" rel="apple-touch-icon">

    <!-- bootstrap CSS -->
    <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.2/css/bootstrap.min.css">

    <!-- custom css -->
    <link href="../assets/css/style.css" rel="stylesheet">
    <link rel="stylesheet" href="https://pro.fontawesome.com/releases/v5.10.0/css/all.css"
          integrity="sha384-AYmEC3Yw5cVb3ZcuHtOA93w35dYTsvhLPVnYs9eStHfGJvOvKxVfELGroGkvsg+p" crossorigin="anonymous"/>

    <!-- IE8 에서 HTML5 요소와 미디어 쿼리를 위한 HTML5 shim 와 Respond.js -->
    <!-- WARNING: Respond.js 는 당신이 file:// 을 통해 페이지를 볼 때는 동작하지 않습니다. -->
    <!--[if lt IE 9]>
    <script src="https://oss.maxcdn.com/html5shiv/3.7.2/html5shiv.min.js"></script>
    <script src="https://oss.maxcdn.com/respond/1.4.2/respond.min.js"></script>
    <![endif]-->
</head>
  <div class="container">

            <h2 class="page-title text-center">Java 클럽 - 회원목록</h2>

            <div class="content">
                <div class="search-form">
                    <form action="">
                        <div class="form-group">
                            <div class="input-group">
                                <input type="text" class="form-control" placeholder="검색어를 입력하세요." v-model="clubname">
                                <div class="input-group-btn">
                                    <button type="button" class="btn btn-primary"><span
                                            class="glyphicon glyphicon-search" @click="onClickSearchBtn"></span></button>
                                </div><!-- /btn-group -->
                            </div><!-- /input-group -->
                        </div>
                    </form>
                </div>

                <div class="row btn-action">
                    <div class="col-sm-12">
                        <div class="fl-right">
                            <!-- trigger modal -->
                            <button class="btn btn-default" data-toggle="modal" data-target="#myModal">
                                <i class="fas fa-plus"></i>
                                등록
                            </button>

                            <!-- Modal -->
                            <div class="modal fade" id="myModal" tabindex="-1" role="dialog" aria-labelledby="myModalLabel"
                                 aria-hidden="true">
                                <div class="modal-dialog">
                                    <div class="modal-content">
                                        <div class="modal-header">
                                            <button type="button" class="close" data-dismiss="modal"
                                                    aria-label="Close"><span
                                                    aria-hidden="true">&times;</span></button>
                                            <h4 class="modal-title" id="myModalLabel">회원등록</h4>
                                        </div>
                                        <div class="modal-body">
                                            <form>
                                                <div class="form-group">
                                                    <label for="exampleInputEmail1">이메일</label>
                                                    <input type="email" class="form-control" id="exampleInputEmail1"
                                                           placeholder="이메일" value="hello@nextree.io">
                                                </div>
                                                <div class="form-group">
                                                    <label for="exampleInputEmail1">이름</label>
                                                    <input type="text" class="form-control" id="exampleInputEmail1"
                                                           placeholder="이름" value="홍길동">
                                                </div>
                                                <div class="form-group">
                                                    <label for="exampleInputPassword1">휴대폰 번호</label>
                                                    <input type="text" class="form-control" id="exampleInputPassword1"
                                                           placeholder="휴대폰 번호" value="010-1234-5678">
                                                </div>
                                            </form>
                                            <div class="row btn-action">
                                                <div class="col-sm-12">
                                                    <div class="fl-right">
                                                        <button class="btn btn-primary btn-bordered">
                                                            <i class="fas fa-check"></i> 등록
                                                        </button>
                                                    </div>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>

                <div class="table-wrap">
                    <table class="table text-center">
                        <thead>
                        <tr>
                            <th class="text-center">No</th>
                            <th class="text-center">클럽 이름</th>
                            <th class="text-center">소개글</th>
                            <th class="text-center">가입일</th>
                            <th class="text-center">회원 수</th>
                            <th class="text-center">권한</th>
                        </tr>
                        </thead>
                        
                        <tbody>
                            <tr v-for="(value, name, index) in clubList" v-bind:key="index">
                                <th scope="row" class="text-center" v-for="(value, name, index) in value" v-bind:key="index">
                                    <td v-if="!(name==='isAdmin')">{{value}}</td>
                                    <td v-else-if="name==='isAdmin'&&value"> 
                                        <div is="sui-button-group">
                                            <sui-button positive>수정</sui-button>
                                            <sui-button-or />
                                            <sui-button >삭제</sui-button>
                                        </div>
                                    </td><td v-else-if="name==='isAdmin'&&!value"> 
                                        <div is="sui-button-group">
                                            <sui-button positive>탈퇴</sui-button>
                                        </div>
                                    </td>
                                </th>
                            </tr>
                        </tbody>
                    </table>
                </div>
                <div class="row btn-action">
                    <div class="col-sm-12">
                        <button class="btn btn-default">
                            <i class="fas fa-list"></i> 목록
                        </button>
                        <div class="fl-right">
                            <button class="btn btn-default btn-bordered">
                                <i class="fas fa-edit"></i> 수정
                            </button>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        </html>
</template>

<script>
 import {findClubs} from '../../api/UserApi.js'
 import {getClubs} from '../../api/UserApi.js'
export default {
    name : "club-list-page",
    data :function(){
        return{
            clubname: "",
            clubList:[{}],
        }
    },
    mounted: async function(){
        this.clubList = await getClubs();
        console.log(JSON.stringify(this.clubList))
    },
    methods:{
        onClickSearchBtn : async function(){
            let clubList = await findClubs(this.clubname)
            this.clubList = clubList
            console.log(JSON.stringify(clubList))
        }
    },
}
</script>

<style>

</style>