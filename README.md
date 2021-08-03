# react-from-hook-b4


# Hook section



       import React from 'react'
       import { useRef } from 'react'
       import { useForm } from "react-hook-form"
       import "./Signup.css"





       const Signup = () => {

    const { register, formState: { errors }, handleSubmit, reset, watch } = useForm()

    const password = useRef({})
    password.current = watch("password", "");

    const onSubmit = (e) => {
        console.log(e);
        reset()

    }

    return (
        <div className="container">
            <div className="row">
                <div className="col-lg-6 offset-lg-3 col-md-8 offset-md-2 col-12">
                    <div className="card signup_Wrapper p-3 my-5">
                    <h4 className="text-center">Signup</h4>
                        <form onSubmit={handleSubmit(onSubmit)}>


                        <div className="input_field_div">

                            <input type="text" className="form-control input_field my-2" {...register("name", {
                                required: "Name is Require", minLength: {
                                    value: 4,
                                    message: "Name mustbe 4 carecter"
                                }
                            })} placeholder="Enter Your Name"></input>
                            </div>
                            {errors.name && (<small style={{ color: "red" }}>{errors.name.message}</small>)}

                            <div className="input_field_div">
                            <input type="email" className="form-control input_field my-2" {...register("email", {
                                required: "Email is Require", pattern: {
                                    value: /^\w+([\.-]?\w+)*@\w+([\.-]?\w+)*(\.\w{2,3})+$/,
                                    message: "Invalid Email Address"
                                }
                            })} placeholder="Enter Your Eamil"></input>
                            </div>
                            {errors.email && (<small style={{ color: "red" }}>{errors.email.message}</small>)}

                            <div className=" input_field_div">
                                  <input type="phone" className="form-control input_field my-2" {...register("phone", {
                                    required: "Phone is Require", min: {
                                        value: 10,
                                        message: "Minimum value is 10"
                                    },
                                    pattern: {
                                        value: /^(?:\+88|88)?(01[3-9]\d{8})$/,
                                        message: "Phone Number is invalid"
                                    }
                                })} placeholder="Enter Your phone"></input>
                            </div>
                            {errors.phone && (<small style={{ color: "red" }}>{errors.phone.message}</small>)}
                            <div className="input_field_div">
                            <input type="password" className="form-control input_field my-2" {...register("password", {
                                required: "Password is Require", minLength: {
                                    value: 8,
                                    message: "Password must have at least 8 characters"
                                }
                            })} placeholder="Enter Your password"></input>
                            </div>
                            {errors.password && (<small style={{ color: "red" }}>{errors.password.message}</small>)}

                            <div className="input_field_div">
                            <input type="password" className="form-control input_field my-2" {...register("cpassword", {
                                required: "Password Not Match", validate: value =>
                                    value === password.current || "The passwords do not match"
                            })} placeholder="Confirm Password"></input>
                            </div>
                            {errors.cpassword && (<small style={{ color: "red" }}>{errors.cpassword.message}</small>)}


                            <br></br>
                            <button className="btn btn-success">Submit</button>
                        </form>
                    </div>
                </div>
            </div>
        </div >
    )
    }

       export default Signup




# CSS section

    .input_field {
    border: none !important;
     }
    .input_field:focus {
    box-shadow: none !important;
     } 
    .input_field_div {
    border-bottom: 1px solid rgba(0, 0, 0, 0.137);
    }
    .signup_Wrapper {
    border-radius: 10px;
    box-shadow: 0px 0px 3px rgba(0, 0, 0, 0.144);
    }
