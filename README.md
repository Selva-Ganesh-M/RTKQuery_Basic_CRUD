# RTKQuery_Basic_CRUD

# api slice

import { createApi, fetchBaseQuery } from "@reduxjs/toolkit/query/react";

const apiSlice = createApi({
reducerPath: "api", //default value.Thus,optional.
baseQuery: fetchBaseQuery({
baseUrl: "http://localhost:3500",
}),
tagTypes: ["Todos"],
endpoints: (builder) => ({
getTodos: builder.query({
query: () => "/todos",
providesTags: ["Todos"],
}),
addTodo: builder.mutation({

        {/*
        the below query method accepts only one argument, you can use objects to advantage to send multiple parameters
        */}

      query: (todo) => ({
        url: "/todos",
        method: "POST",
        body: todo,
      }),
      invalidatesTags: ["Todos"],
    }),
    updateTodo: builder.mutation({
      query: (todo) => ({
        url: `/todos/${todo.id}`,
        method: "PATCH",
        body: todo,
      }),
      invalidatesTags: ["Todos"],
    }),
    deleteTodo: builder.mutation({
      query: (id) => ({
        url: `/todos/${id}`,
        method: "DELETE",
      }),
      invalidatesTags: ["Todos"],
    }),

}),
});

export const {
useGetTodosQuery,
useAddTodoMutation,
useUpdateTodoMutation,
useDeleteTodoMutation,
} = apiSlice;
export default apiSlice;

# index.js

import { ApiProvider } from "@reduxjs/toolkit/query/react";
import apiSlice from "./features/api/apiSlice";

ReactDOM.createRoot(document.getElementById("root")).render(
<React.StrictMode>
<ApiProvider api={apiSlice}>
<App />
</ApiProvider>
</React.StrictMode>
);

# usage

const {
data: todos,
isLoading,
isError,
isSuccess,
error,
} = useGetTodosQuery();
const [addTodo] = useAddTodoMutation();
const [updateTodo] = useUpdateTodoMutation();
const [deleteTodo] = useDeleteTodoMutation();

# add new todo

addTodo({
userId: 1,
title: newTodo,
completed: false,
});
